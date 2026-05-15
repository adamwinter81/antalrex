# Dokumentacja: remove-user.yml

## Cel
Playbook `remove-user.yml` służy do usuwania wskazanego użytkownika oraz jego katalogu domowego na wszystkich hostach zarządzanych przez Ansible.

## Lokalizacja
```
/ANSIBLE/playbooks/remove-user.yml
```
## Parametry
- `user_to_remove` (**wymagany**): nazwa użytkownika do usunięcia (nie jest hardkodowana, podawana jako parametr).
- `dry_run` (opcjonalny, domyślnie `false`): jeśli ustawiony na `true`, playbook działa w trybie "na sucho" (dry-run) – nie usuwa użytkownika, tylko sprawdza jego obecność.

## Wywołanie
Usuń użytkownika:
```bash
ansible-playbook /ANSIBLE/playbooks/remove-user.yml -e user_to_remove=NAZWA_UZYTKOWNIKA
```
Tryb sprawdzania (dry-run):
```bash
ansible-playbook /ANSIBLE/playbooks/remove-user.yml -e user_to_remove=NAZWA_UZYTKOWNIKA -e dry_run=true
```
## Działanie
1. Sprawdza, czy użytkownik istnieje na danym hoście.
2. Jeśli `dry_run=true`, wyświetla informację o obecności użytkownika, nie wykonuje żadnych zmian.
3. Jeśli `dry_run=false` (domyślnie), usuwa użytkownika oraz jego katalog domowy, jeśli istnieje.

## Przykład
Usunięcie użytkownika `kpala`:
```bash
ansible-playbook /ANSIBLE/playbooks/remove-user.yml -e user_to_remove=kpala
```
Sprawdzenie obecności użytkownika `kpala` bez usuwania:
```bash
ansible-playbook /ANSIBLE/playbooks/remove-user.yml -e user_to_remove=kpala -e dry_run=true
```
## Uwagi
- Playbook wymaga uprawnień root (become: yes lub uruchomienie jako root).
- Nazwa użytkownika przekazywana jest dynamicznie przez parametr `user_to_remove`.
- Playbook nie modyfikuje innych kont ani plików poza wskazanym użytkownikiem.
# Dokumentacja: remove-user.yml

## Cel
Playbook `remove-user.yml` służy do usuwania wskazanego użytkownika oraz jego katalogu domowego na wszystkich hostach zarządzanych przez Ansible.

## Lokalizacja
```
/ANSIBLE/playbooks/remove-user.yml
```

## Parametry
- `user_to_remove` (**wymagany**): nazwa użytkownika do usunięcia (nie jest hardkodowana, podawana jako parametr).
- `check_mode` (opcjonalny, domyślnie `false`): jeśli ustawiony na `true`, playbook działa w trybie "na sucho" (dry-run) – nie usuwa użytkownika, tylko sprawdza jego obecność.

## Wywołanie
Usuń użytkownika:
```bash
ansible-playbook /ANSIBLE/playbooks/remove-user.yml -e user_to_remove=NAZWA_UZYTKOWNIKA
```

Tryb sprawdzania (dry-run):
```bash
ansible-playbook /ANSIBLE/playbooks/remove-user.yml -e user_to_remove=NAZWA_UZYTKOWNIKA -e check_mode=true
```

## Działanie
1. Sprawdza, czy użytkownik istnieje na danym hoście.
2. Jeśli `check_mode=true`, wyświetla informację o obecności użytkownika, nie wykonuje żadnych zmian.
3. Jeśli `check_mode=false` (domyślnie), usuwa użytkownika oraz jego katalog domowy, jeśli istnieje.

## Przykład
Usunięcie użytkownika `kpala`:
```bash
ansible-playbook /ANSIBLE/playbooks/remove-user.yml -e user_to_remove=kpala
```

Sprawdzenie obecności użytkownika `kpala` bez usuwania:
```bash
c```

## Uwagi
- Playbook wymaga uprawnień root (become: yes).
- Nazwa użytkownika przekazywana jest dynamicznie przez parametr `user_to_remove`.
- Playbook nie modyfikuje innych kont ani plików poza wskazanym użytkownikiem.
