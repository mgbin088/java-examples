# Spring Boot 动态规则引擎 Demo

## 项目简介

这是一个基于 **Spring Boot + QLExpress** 的动态规则引擎演示项目，展示如何在不重启应用的情况下动态修改业务规则。项目采用前后端分离架构，使用 TailwindCSS 构建现代化的管理界面。

## 🚀 核心功能

- **动态规则管理** - 运行时加载、修改、删除业务规则
- **前后端分离** - REST API + 现代化前端界面
- **业务场景演示** - 完整的电商订单处理流程
- **热更新支持** - 无需重启应用即可修改规则逻辑
- **可视化管理** - 直观的规则管理和测试界面

## 🎯 解决的痛点

**传统方式的问题：**
- 业务规则变更需要修改代码、重新编译、发布部署
- 营销活动、风控策略等频繁变化的规则维护成本高
- 无法快速响应业务需求变化

**动态规则引擎的优势：**
- ✅ 规则热更新，无需重启应用
- ✅ 业务人员可直接配置规则
- ✅ 快速响应营销活动需求
- ✅ 降低运维成本和风险

## 🛠 技术栈

- **后端：** Spring Boot 3.2.0, QLExpress 3.3.1
- **前端：** HTML5 + JavaScript + TailwindCSS

## 📋 业务场景演示

### 电商订单处理流程

项目通过一个完整的电商订单处理场景，展示动态规则引擎的实际应用：

1. **VIP折扣规则** - 根据用户等级应用不同折扣
2. **满减活动规则** - 满足条件时自动减免金额
3. **积分奖励规则** - 基于最终金额计算积分

### 预置规则示例

#### VIP折扣规则 (`vip_discount`)
```javascript
if (userLevel == "GOLD") {
    return price * 0.8;
} else if (userLevel == "SILVER") {
    return price * 0.9;
} else {
    return price;
}
```

#### 满减活动规则 (`full_reduction`)
```javascript
if (totalAmount >= 200) {
    return totalAmount - 50;
} else if (totalAmount >= 100) {
    return totalAmount - 20;
} else {
    return totalAmount;
}
```

#### 积分奖励规则 (`points_reward`)
```javascript
return Math.round(totalAmount * 0.1);
```

## 🚀 快速开始

### 1. 启动应用
```bash
git clone <repository-url>
cd springboot-dynamic-rule
mvn spring-boot:run
```

### 2. 访问应用
- **规则管理页面：** http://localhost:8080/index.html
- **业务演示页面：** http://localhost:8080/business.html

### 3. 体验功能
1. 在规则管理页面查看和测试规则
2. 在业务演示页面模拟订单处理
3. 动态修改规则并观察业务逻辑变化

## 📡 API 接口

### 规则管理 API
```bash
GET    /api/rules                 # 获取所有规则
POST   /api/rules                 # 添加新规则
PUT    /api/rules/{ruleName}      # 更新规则
DELETE /api/rules/{ruleName}      # 删除规则
POST   /api/rules/execute/{name}  # 执行规则
```

### 业务演示 API
```bash
POST /api/orders/simulate?userLevel={level}&amount={amount}  # 模拟订单处理
POST /api/orders/process     # 处理订单
```

### 示例请求
```bash
# 执行VIP折扣规则
curl -X POST http://localhost:8080/api/rules/execute/vip_discount \
  -H "Content-Type: application/json" \
  -d '{"userLevel": "GOLD", "price": 100}'

# 模拟订单处理
curl -X POST "http://localhost:8080/api/orders/simulate?userLevel=GOLD&amount=150"
```
