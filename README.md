# Kubernetes MySQL 主從複製部署

## 說明

- 適用於測試環境
- 適用於本地開發環境
- 不安全預設值，在生產環境中使用時，請確保正確配置安全性設置
- 適用於 Kubernetes 集群

## 功能

- 自動部署 MySQL 主從複製架構
- 支持動態擴展從節點
- 使用 StatefulSet 確保數據持久性和穩定性
- 自動初始化從節點並配置主從複製
- 使用 ConfigMap 管理 MySQL 配置

## 實現方法

1. **StatefulSet**：使用 StatefulSet 部署 MySQL 實例，確保穩定的網絡標識和存儲。

2. **初始化容器**：
   - `init-mysql`：設置 MySQL 服務器 ID 和配置文件。
   - `clone-mysql`：從主節點克隆數據到從節點。

3. **xtrabackup**：使用 Percona XtraBackup 進行數據備份和恢復。

4. **動態配置**：使用 bash 腳本動態生成 MySQL 配置和複製設置。


## 使用方法

1. 克隆此存儲庫：
   ```
   git clone https://github.com/Elliot9/k8s-mysql-master-slave.git
   ```

2. 應用 PersistentVolume 配置：
   ```
   kubectl apply -f pv.yaml
   ```

3. 創建 ConfigMap：
   ```
   kubectl apply -f mysql-config.yaml
   ```

4. 部署 MySQL StatefulSet：
   ```
   kubectl apply -f mysql-statefulset.yaml
   ```

5. 創建 MySQL 服務：
   ```
   kubectl apply -f mysql-service.yaml
   ```
