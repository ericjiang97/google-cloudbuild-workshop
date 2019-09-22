# Did **you** know?

---

### *We only have* 500 build mins per months *for BitBucket Pipelines (CI/CD)*



---

# In comes cloud build

* Still CI/CD
* Triggers can be set to Repository Sources such as BitBucket, GitHub, etc.
* Native to Google Cloud Platform, means no need to specify service accounts, etc.

![left 90%](https://cloud.google.com/images/products/cloud-build/cloud-build.png)

---

# Reporting from cloud build

1. Create trigger that listens push to target to branch for example (every branch other than `develop`, `staging` and `master`)

2. Run test step

3. Use Pub/Sub that listens to the `cloud-builds` trigger

4. Use Google Cloud Functions that gets triggered by the `cloud-builds` Pub/Sub event

5. Report status via GCF to BitBucket via the BitBucket API

---


![80%](https://i.imgur.com/UTGaG0O.png)


---

# For example, testing branches

_/cloud-build/test-branch.yaml_

```
steps:
  # Install Backend
  - name: "gcr.io/cloud-builders/npm:node-10.10.0"
    args: ["install"]

  # Test Backend
  - name: "gcr.io/cloud-builders/npm:node-10.10.0"
    args: ["test"]

  # Install Frontend
  - name: "gcr.io/cloud-builders/npm:node-10.10.0"
    args: ["install"]
    dir: frontend

  # Test Frontend
  - name: "gcr.io/cloud-builders/npm:node-10.10.0"
    args: ["run", "tefrontendst:ci"]
    dir: 

```

--- 

