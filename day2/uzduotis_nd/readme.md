# Namų darbas: Podinfo diegimas su FluxCD Helm Controller

## Tikslas

Įdiegti **FluxCD Helm Controller** ir **Source Controller** savo Kubernetes klasteryje naudojant FluxCD. Programėlė turi būti pasiekiama šiuo URL formatu: `https://stud<Nr>.devplay.art`

Pakeiskite `<Nr>` į jums priskirtą studento numerį.

---

## Reikalavimai

1. **Kubernetes klasteris** - užtikrinkite prieigą prie klasterio.
2. **kubectl** - įdiegta ir sukonfigūruota klasteriui.
3. **FluxCD CLI** - [Įdiegimo instrukcija](https://fluxcd.io/flux/get-started/#install-the-flux-cli)

---

## 1 žingsnis: FluxCD Helm Controller ir Source Controller diegimas

Vadovaukitės oficialiomis diegimo instrukcijomis:
- [Helm Controller](https://fluxcd.io/flux/components/helm/helmreleases/#helm-controller)
- [Source Controller](https://fluxcd.io/flux/components/source/)

Diegimas:
```bash
flux install \
  --components=source-controller,helm-controller
```

Patikrinkite ar viskas veikia:

```bash
kubectl get pods -n flux-system
```

---

## 2 žingsnis: Sukurkite HelmRepository ir HelmRelease

Sukurkite failą `podinfo-helmrelease.yaml` su šiuo turiniu savo sukurtame kataloge ir pakeiskite reikšmes pagal reikiamus reikalavimus:

>**Svarbu!** Pakeiskite `<Nr>` į savo studento numerį. Pvz. `stud1.devplay.art`

```yaml
apiVersion: source.toolkit.fluxcd.io/v1
kind: HelmRepository
metadata:
  name: podinfo
  namespace: stud<Nr>-podinfo
spec:
  interval: 10m0s
  url: https://stefanprodan.github.io/podinfo
---
apiVersion: helm.toolkit.fluxcd.io/v2
kind: HelmRelease
metadata:
  name: podinfo
  namespace: stud<Nr>-podinfo
spec:
  chart:
    spec:
      chart: podinfo
      sourceRef:
        kind: HelmRepository
        name: podinfo
      version: '6.0.0'
  interval: 10m0s
  values:
    replicaCount: 2
    ingress:
      enabled: true
      className: "nginx"
      hosts:
        - host: stud<Nr>.devplay.art
          paths:
            - path: /
              pathType: Prefix

```

---

## 3 žingsnis: Taikykite konfigūraciją

Paleiskite programėlę naudodami FluxCD:
```bash
kubectl apply -f podinfo-helmrelease.yaml
```

Patikrinkite diegimo būseną:
```bash
kubectl get helmrelease -A
```

---

## 4 žingsnis: Patikrinkite diegimą

Aplankykite programėlę naršyklėje:
```
https://stud<Nr>.devplay.art
```
Įsitikinkite, kad DNS nukreipia į jūsų Kubernetes klasterį.

---

## 5 žingsnis: Išvalykite diegimą

Norėdami pašalinti diegimą:
```bash
kubectl delete -f podinfo-helmrelease.yaml
```

---

**Sėkmės diegiant!**

