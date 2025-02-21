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
- `podinfo` Helm Chart puslapyje dešiniajam kampe suraskite `Source` nuorodą
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
- Pakeiskite resursus reikalingus įsidiegti ir pasiekti `podinfo` aplikaciją naudojant subdomeną **`stud<nr>.devplay.art`**
  `podinfo/podinfo/charts/podinfo/values.yaml`

  ```sh
  helm install my-podinfo podinfo/podinfo --version 6.7.1 --values=./values.yaml --namespace stud<nr>-podinfo --create-namespace
  ```

  Jei reikia nuorodyti kur config failas:
  
  ```bash
  helm install <release-name> <chart-name> --kubeconfig <path-to-kubeconfig>
   ```

  ```bash
  helm install my-release my-chart \
  --kubeconfig ~/.kube/custom-config \
  --namespace my-namespace \
  --set key1=value1,key2=value2
  ```

### 6. Patikrinkite Service, Pod ir Ingress
```sh
kubectl get all -n podinfo
```

### 7. Įdiekite FluxCD Source ir Helm operatorių
 Jei reikia pašalinti nereikalingus komponentus, naudokite `--components=`:

 ```sh
flux install --components="helm-controller,source-controller"
```

Pašalinti flux

```sh
flux uninstall
```

