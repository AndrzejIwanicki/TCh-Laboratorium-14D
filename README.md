# TCh-Laboratorium-14D

W celu zabezpieczenia danych wrażliwych zmodyfikowano architekturę aplikacji:
1. Usunięto jawne wartości haseł z sekcji environment w pliku docker-compose.yml.
2. Utworzono pliki tekstowe w katalogu ./secrets/ przechowujące hasła.
3. Wykorzystano mechanizm top-level secrets do zmapowania plików na sekrety Dockera.
4. Przekazano hasła do kontenerów mysql oraz phpmyadmin przy użyciu zmiennych z przyrostkiem _FILE (np. MYSQL_ROOT_PASSWORD_FILE), które automatycznie odczytują zawartość bezpiecznie montowaną w katalogu /run/secrets/.

Weryfikacja poleceniem docker inspect lemp_mysql potwierdza poprawne powiązanie sekretów z bazą danych w trybie tylko do odczytu:

```
            {
                "Type": "bind",
                "Source": "C:\\Users\\PC\\laby\\lab14\\secrets\\db_password.txt",
                "Destination": "/run/secrets/db_password",
                "Mode": "",
                "RW": false,
                "Propagation": "rprivate"
            },
            {
                "Type": "bind",
                "Source": "C:\\Users\\PC\\laby\\lab14\\secrets\\db_root_password.txt",
                "Destination": "/run/secrets/db_root_password",
                "Mode": "",
                "RW": false,
                "Propagation": "rprivate"
            }
