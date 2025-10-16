In .env files never use "" just type the keys plain

Conventions
- Main branch gebruiken deze moet altijd een werkende versie bevatten
- Geen gevoelige data publiceren
- Zorg ervoor dat de commit messages en omschrijvingen duidelijk zijn.
- Zorg voor een README.md met een duidelijke omschrijving. 

New repository.

1. git init in project
    als je uv init doet dan doet hij dit automatisch
2. create repo in Github
    naming convention is kebab case. begin met klant naam dan project dan soort
3. vervolgens de repo's linken
    git remote add origin https://github.com/Bolk-Business-Improvements/bbi-dock-management-python-sdk.git
4. branch naam op main zetten ipv master (convention)
    git branch -M main
5. vervolgens kun je in github desktop de repo toevoegen door proberen repo te selecteren -> add -> Add existing repo... -> selecteer map waarin je de git init hebt gedraaid.
6. nu kun je bestanden toevoegen aan de repository goed controleren dat je geen gevoelige informatie toevoegd bijv .env
7. Nadat je je eerste versie hebt gepubliceerd is het vaak handig om in een development branch te gaan.
