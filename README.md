# -Skrypt-Linux
```python
#!/bin/bash

search_files() {
    folder="$1"
    keyword="$2"
    files=$(find "$folder" -type f -name "*.txt" -exec grep -l "$keyword" {} +)
    for file in $files; do
        remove_last_line "$file"
    done
}

remove_last_line() {
    file="$1"
    sed -i '$d' "$file"
}

while true; do
    echo "Menu:"
    echo "1. Wyszukaj pliki tekstowe w folderze"
    echo "2. Usuń ostatnią linię zapisanego tekstu w plikach"
    echo "3. Zabij 5 losowych procesów działających w tle"
    echo "4. Imię Autora"
    echo "5. Wyjdź"

    read -p "Wybierz opcję: " option

    case $option in
        1)
            read -p "Podaj ścieżkę do folderu: " folder
            read -p "Podaj słowo kluczowe: " keyword
            search_files "$folder" "$keyword"
            echo "Zakończono wyszukiwanie i usuwanie ostatniej linii z plików tekstowych."
            ;;
        2)
            read -p "Podaj ścieżkę do folderu: " folder
            read -p "Podaj słowo kluczowe: " keyword
            search_files "$folder" "$keyword"
            echo "Zakończono usuwanie ostatniej linii z plików tekstowych."
            ;;
        3)
            echo "Zabijanie 5 losowych procesów działających w tle..."
            pids=$(ps aux | awk '{print $2}' | shuf -n 5)
            for pid in $pids; do
                kill "$pid"
            done
            echo "Zakończono zabijanie procesów."
            ;;
        4)
            echo "Nikodem Wyka"
            ;;
        5)
            echo "Do widzenia!"
            exit 0
            ;;
        *)
            echo "Nieprawidłowa opcja. Wybierz ponownie."
            ;;
    esac

    echo
done
```
