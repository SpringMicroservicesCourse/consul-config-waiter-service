# Consul Config Waiter Service ⚡

[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.5-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Spring Cloud](https://img.shields.io/badge/Spring%20Cloud-2024.0.2-blue.svg)](https://spring.io/projects/spring-cloud)
[![Consul](https://img.shields.io/badge/Consul-Config%20Center-purple.svg)](https://www.consul.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 專案介紹

這是一個基於 Spring Boot 3.x 和 Spring Cloud 2024.x 的微服務專案，主要展示如何使用 **Consul** 作為配置中心來管理服務配置。專案實現了一個咖啡廳服務員系統，包含咖啡管理、訂單處理等功能。

> 💡 **為什麼選擇 Consul 作為配置中心？**
> - **動態配置更新**：無需重啟服務即可更新配置
> - **多格式支援**：支援 Key-Value、YAML、JSON 等多種配置格式
> - **服務發現整合**：與 Consul 服務發現功能完美整合
> - **高可用性**：Consul 叢集提供高可用性保障

### 🎯 專案特色

- **動態配置管理**：透過 Consul 實現配置的動態更新
- **服務註冊與發現**：自動註冊到 Consul 服務目錄
- **熔斷與限流**：整合 Resilience4j 實現服務保護
- **監控與指標**：提供完整的健康檢查和監控端點
- **台灣在地化**：使用台灣常用專業術語，符合本地開發習慣

## 技術棧

### 核心框架
- **Spring Boot 3.4.5** - 現代化 Java 應用程式框架
- **Spring Cloud 2024.0.2** - 微服務架構解決方案
- **Spring Data JPA** - 資料持久化層
- **Hibernate 6** - ORM 框架

### 微服務組件
- **Spring Cloud Consul Config** - Consul 配置中心整合
- **Spring Cloud Consul Discovery** - 服務註冊與發現
- **Resilience4j** - 服務熔斷與限流
- **Micrometer** - 應用程式監控指標

### 開發工具與輔助
- **Maven** - 專案建置與依賴管理
- **H2 Database** - 內嵌式資料庫（開發環境）
- **Lombok** - 減少樣板程式碼
- **Joda Money** - 貨幣處理工具

## 專案結構

```
consul-config-waiter-service/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── tw/fengqing/spring/springbucks/waiter/
│   │   │       ├── WaiterServiceApplication.java          # 主應用程式類別
│   │   │       ├── controller/                            # 控制器層
│   │   │       │   ├── CoffeeController.java             # 咖啡管理 API
│   │   │       │   ├── CoffeeOrderController.java        # 訂單管理 API
│   │   │       │   ├── PerformanceInteceptor.java        # 效能監控攔截器
│   │   │       │   └── request/                          # 請求物件
│   │   │       ├── model/                                # 資料模型層
│   │   │       │   ├── BaseEntity.java                   # 基礎實體類別
│   │   │       │   ├── Coffee.java                       # 咖啡實體
│   │   │       │   ├── CoffeeOrder.java                  # 訂單實體
│   │   │       │   ├── OrderState.java                   # 訂單狀態列舉
│   │   │       │   └── MoneyConverter.java               # 貨幣轉換器
│   │   │       ├── repository/                           # 資料存取層
│   │   │       │   ├── CoffeeRepository.java             # 咖啡資料存取
│   │   │       │   └── CoffeeOrderRepository.java        # 訂單資料存取
│   │   │       ├── service/                              # 業務邏輯層
│   │   │       │   ├── CoffeeService.java                # 咖啡業務邏輯
│   │   │       │   └── CoffeeOrderService.java           # 訂單業務邏輯
│   │   │       └── support/                              # 支援組件
│   │   │           ├── CoffeeIndicator.java              # 健康檢查指標
│   │   │           ├── OrderProperties.java              # 訂單配置屬性
│   │   │           ├── MoneySerializer.java              # 貨幣序列化器
│   │   │           ├── MoneyDeserializer.java            # 貨幣反序列化器
│   │   │           └── MoneyFormatter.java               # 貨幣格式化器
│   │   └── resources/
│   │       ├── application.properties                    # 應用程式配置
│   │       ├── bootstrap.properties                      # 啟動配置（Consul 設定）
│   │       ├── schema.sql                                # 資料庫結構
│   │       ├── data.sql                                  # 初始資料
│   │       └── coffee.txt                                # 咖啡資料檔案
│   └── test/
│       └── java/
│           └── tw/fengqing/spring/springbucks/waiter/
│               └── WaiterServiceApplicationTests.java    # 應用程式測試
├── pom.xml                                               # Maven 專案配置
└── README.md                                             # 專案說明文件
```

## 快速開始

### 前置需求
- **Java 21** 或更高版本
- **Maven 3.6** 或更高版本
- **Consul 服務**（本地或遠端）
- **Docker**（可選，用於啟動 Consul）

### 安裝與執行

1. **啟動 Consul 服務：**
```bash
# 使用 Docker 啟動 Consul
docker run -d --name consul -p 8500:8500 consul:latest

# 或使用本地安裝的 Consul
consul agent -dev
```

2. **克隆此專案：**
```bash
git clone <repository-url>
cd consul-config-waiter-service
```

3. **編譯專案：**
```bash
mvn clean compile
```

4. **執行應用程式：**
```bash
mvn spring-boot:run
```

5. **驗證服務啟動：**
```bash
# 檢查健康狀態
curl http://localhost:8080/actuator/health

# 查看所有咖啡
curl http://localhost:8080/coffee/

# 創建訂單
curl -X POST http://localhost:8080/order/ \
  -H "Content-Type: application/json" \
  -d '{"customer":"張三","items":["espresso","latte"]}'
```

## Consul 配置管理

### 配置結構
在 Consul 中，配置按照以下路徑組織：
```
config/
├── application/          # 全域配置
│   └── data
└── waiter-service/       # 服務特定配置
    └── data
```

### 配置範例
在 Consul UI 中建立以下配置：

**路徑：** `config/waiter-service/data`
**格式：** YAML
```yaml
order:
  discount: 65
  waiter-prefix: "fengqing-"
```

修改配置
```yaml
order:
  discount: 60
  waiter-prefix: "fengqing-"
```

### 動態配置更新
1. 在 Consul UI 中修改配置值
2. 系統會自動檢測變更（預設每秒檢查一次）
3. 配置變更會自動生效，無需重啟服務

## 進階說明

### 環境變數
```properties
# Consul 連線設定
CONSUL_HOST=localhost
CONSUL_PORT=8500

# 應用程式設定
SERVER_PORT=8080
SPRING_PROFILES_ACTIVE=default
```

### 設定檔說明

#### bootstrap.properties
```properties
# 應用程式名稱
spring.application.name=waiter-service

# Consul 連線設定
spring.cloud.consul.host=localhost
spring.cloud.consul.port=8500
spring.cloud.consul.discovery.prefer-ip-address=true

# Consul 配置中心設定
spring.cloud.consul.config.enabled=true
spring.cloud.consul.config.format=yaml
```

#### application.properties
```properties
# JPA 設定
spring.jpa.hibernate.ddl-auto=none
spring.jpa.properties.hibernate.show_sql=true

# 監控端點設定
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always

# Resilience4j 限流設定
resilience4j.ratelimiter.instances.coffee.limit-for-period=5
resilience4j.ratelimiter.instances.order.limit-for-period=3
```

## API 端點

### 咖啡管理
- `GET /coffee/` - 取得所有咖啡
- `GET /coffee/{id}` - 取得指定咖啡
- `GET /coffee/?name={name}` - 依名稱查詢咖啡
- `POST /coffee/` - 新增咖啡

### 訂單管理
- `GET /order/{id}` - 取得指定訂單
- `POST /order/` - 建立新訂單

### 監控端點
- `GET /actuator/health` - 健康檢查
- `GET /actuator/info` - 應用程式資訊
- `GET /actuator/metrics` - 監控指標

## 參考資源

- [Spring Boot 官方文件](https://spring.io/projects/spring-boot)
- [Spring Cloud Consul 官方文件](https://spring.io/projects/spring-cloud-consul)
- [Consul 官方文件](https://www.consul.io/docs)
- [Resilience4j 官方文件](https://resilience4j.readme.io/)

## 注意事項與最佳實踐

### ⚠️ 重要提醒

| 項目 | 說明 | 建議做法 |
|------|------|----------|
| 配置安全性 | Consul 配置存取控制 | 使用 ACL 和 TLS 加密 |
| 服務發現 | 服務註冊與健康檢查 | 設定適當的健康檢查間隔 |
| 配置更新 | 動態配置變更 | 使用 @RefreshScope 註解 |
| 效能監控 | 應用程式效能追蹤 | 啟用 Micrometer 指標收集 |

### 🔒 最佳實踐指南

- **配置管理**：將敏感資訊存放在環境變數中，一般配置放在 Consul
- **服務註冊**：確保服務名稱唯一，避免衝突
- **健康檢查**：實作自定義健康檢查指標
- **錯誤處理**：使用 Resilience4j 進行熔斷和限流
- **日誌記錄**：使用結構化日誌，便於問題排查

### 💡 開發建議

- **程式碼註解**：在重要的程式碼區塊添加清楚註解，方便團隊成員理解與維護
- **台灣在地化**：使用台灣常用的專業術語，確保溝通順暢且符合本地習慣
- **測試覆蓋**：為核心業務邏輯撰寫單元測試和整合測試
- **文件維護**：及時更新 API 文件和配置說明

## 授權說明

本專案採用 MIT 授權條款，詳見 LICENSE 檔案。

## 關於我們

我們主要專注在敏捷專案管理、物聯網（IoT）應用開發和領域驅動設計（DDD）。喜歡把先進技術和實務經驗結合，打造好用又靈活的軟體解決方案。

## 聯繫我們

- **FB 粉絲頁**：[風清雲談 | Facebook](https://www.facebook.com/profile.php?id=61576838896062)
- **LinkedIn**：[linkedin.com/in/chu-kuo-lung](https://www.linkedin.com/in/chu-kuo-lung)
- **YouTube 頻道**：[雲談風清 - YouTube](https://www.youtube.com/channel/UCXDqLTdCMiCJ1j8xGRfwEig)
- **風清雲談 部落格**：[風清雲談](https://blog.fengqing.tw/)
- **電子郵件**：[fengqing.tw@gmail.com](mailto:fengqing.tw@gmail.com)

---

**📅 最後更新：2025年9月1日**  
**👨‍💻 維護者：風清雲談團隊**
