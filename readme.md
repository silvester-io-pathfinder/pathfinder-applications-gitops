### Sealing Secrets
Because we're running on GCP, we need to seal secrets in offline mode, for which we need the controller's certificate.

```
#List the names of secrets running in kube-system, find the sealed-secret-key one.
kubectl get secrets -n kube-system 

#Use the name to fetch the secret's data.
kubectl get secret sealed-secrets-keylv8cz -n kube-system --template "{{.data}}"
```

Base64 decode the `tls.crt` property and insert it into kubeseal:
```
kubeseal --cert=tls.txt <unsealed.yaml >sealed.yaml -o yaml 
```