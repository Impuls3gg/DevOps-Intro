# Lab 7 Submission

## Task 1: Git State Reconciliation

### Initial State
```bash
version: 1.0
app: myapp
replicas: 3
```

### Drift Detection Output
```bash
$ ./reconcile.sh
Thu Mar 19 15:16:34 RTZ 2026 - DRIFT DETECTED!
Reconciling current state with desired state...
Thu Mar 19 15:16:34 RTZ 2026 - Reconciliation complete
```

### Synchronized Output
```bash
version: 1.0
app: myapp
replicas: 3
```

### Analysis
**Explain the GitOps reconciliation loop:**
Скрипт сравнивает желаемое (Git) и текущее состояние. Если они отличаются, скрипт принудительно копирует желаемое состояние поверх текущего. Это гарантирует, что система всегда соответствует конфигурации.

**Reflection:**
*Imperative (императивный подход) требует точных команд "сделай это, потом это". Declarative (декларативный) просто описывает "я хочу 3 реплики", и система сама решает, как это сделать и как поддерживать это число. Это надежнее, так как система самовосстанавливается.*

## Task 2: GitOps Health Monitoring

### Healthcheck Script
```bash
#!/bin/bash
# healthcheck.sh - Monitor GitOps sync health

DESIRED_MD5=$(md5sum desired-state.txt | awk '{print $1}')
CURRENT_MD5=$(md5sum current-state.txt | awk '{print $1}')

if [ "$DESIRED_MD5" != "$CURRENT_MD5" ]; then
    echo "$(date) - CRITICAL: State mismatch detected!" | tee -a health.log
    echo "  Desired MD5: $DESIRED_MD5" | tee -a health.log
    echo "  Current MD5: $CURRENT_MD5" | tee -a health.log
else
    echo "$(date) - OK: States synchronized" | tee -a health.log
fi
```

### Log Outputs
```bash
Thu Mar 19 15:18:29 RTZ 2026 - OK: States synchronized
Thu Mar 19 15:18:41 RTZ 2026 - CRITICAL: State mismatch detected!
  Desired MD5: a15a1a4f965ecd8f9e23a33a6b543155
  Current MD5: 48168ff3ab5ffc0214e81c7e2ee356f5
Thu Mar 19 15:18:47 RTZ 2026 - OK: States synchronized
Thu Mar 19 15:19:26 RTZ 2026 - OK: States synchronized
Thu Mar 19 15:19:30 RTZ 2026 - OK: States synchronized
```

### Analysis
**How do checksums help?**
*Сравнивая хеши, мы можем мгновенно понять, отличаются ли файлы, не читая их построчно.*

**Comparison with ArgoCD:**
*Это работает точно так же, как "Sync Status" в ArgoCD. Если хеши Git и кластера совпадают — статус "Synced". Если нет — "OutOfSync".*