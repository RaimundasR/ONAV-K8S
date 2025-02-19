# Kubernetes Ingress & Service for Podinfo

## 📝 Užduotis
Sukurti ir pritaikyti **Ingress** bei **Service** resursus, remiantis `podinfo` diegimo (`Deployment`) YAML failu. 

### ✅ Reikalavimai:
1. **Service** turi nukreipti srautą į `podinfo` Deployment konteinerį.
2. **Ingress** turi priimti užklausas per **nginx** Ingress valdiklį (`ingress-nginx`).
3. **Naudojamas subdomenas**: `stud<nr>.devplay.art`, kur `<nr>` yra jūsų numeris.
4. **Service** ir **Ingress** resursai turi būti išdėstyti pvz --> `tavo-namespace-podinfo` (stud1-podinfo) vardinėje srityje (**namespace**).

---

## 📂 (Hints) paaiškinimas

`service`

port: 80 – Išorinis paslaugos prievadas.
targetPort: 9898 – Konteinerio prievadas viduje.

selector: app: podinfo – Susieja su podinfo Deployment. :point_down:

````
metadata:
  name: podinfo-service
  namespace: `tavo-namespace-podinfo` 
spec:
  selector:
    app: podinfo
```



