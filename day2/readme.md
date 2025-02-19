# Praktinė užduotis: Helm ir Git naudojimas

## Užduotis

### 1. Atsisiųsti Git repozitoriją lokaliai į savo kompiuterį
Vykdykite šią komandą terminale:
```sh
git clone https://github.com/RaimundasR/ONAV-K8S.git
```

### 2. Sukurti asmeninį katalogą `day2` kataloge
- Atsidarykite `ONAV-K8S` katalogą:
  ```sh
  cd ONAV-K8S/day2
  ```
- Sukurkite katalogą savo vardu ir pavarde (be tarpų, naudokite `_` arba `-`):
  ```sh
  mkdir <vardaspavarde>
  ```

### 3. Rasti aplikaciją `podinfo` Helm Chart kataloge
- Eikite į [Artifact Hub](https://artifacthub.io/)
- Paieškoje įveskite **podinfo**
- Suraskite repozitorijos savininką **stefanprodan**

### 4. Atsidaryti `podinfo` repozitoriją
- `podinfo` Helm Chart puslapyje dešiniajame kampe suraskite `Source` nuorodą
- Paspauskite ją – ji atsidarys `GitHub` repozitorijoje

### 5. Atsisiųsti `podinfo` repozitoriją į savo katalogą
- Grįžkite į terminalą ir eikite į savo katalogą:
  ```sh
  cd ONAV-K8S/day2/<vardaspavarde>
  ```
- Nuklonuokite `podinfo` repozitoriją:
  ```sh
  git clone https://github.com/stefanprodan/podinfo.git
  ```

