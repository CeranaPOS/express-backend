# Installation
Ensure you have node 16
```console
$ git clone https://github.com/CeranaPOS/express-backend.git
$ cd express-backend
$ npm install
```
# Local Run
1. 架設本地端MySQL
2. 設置.env檔
```bash
# .env
DB_HOST = "your local host"
DB_POST = 3306
DB_USERNAME = "your db username"
DB_PASSWORD = "your db password"
DB_NAME = "your schema name"
```
```console
$ npm run start
```
# API

## Sign up

| Method | Path           |
| ------ | -------------- |
| `POST` | `users/signup` |

### Parameters

* `username` `(string: <required>)` - 使用者名稱
* `password` `(string: <required>)` - 密碼
* `email` `(string: <optional>)` - 使用者Email
* `phoneNumber` `(string: <optional>)` - 使用者電話號碼

### Responses

* `success` `(bool)` - True/False.
* `message` `(string: <success>)` - "註冊成功"
* `err` `(string: <not success>)` - Error message.

---

## Login

| Method | Path          |
| ------ | ------------- |
| `POST` | `users/login` |

### Parameters

* `username` `(string: <required>)` - 使用者名稱
* `password` `(string: <required>)` - 密碼

### Responses

* `success` `(bool)` - True/False.
* `userId` `(string: <success>)` - 使用者Id
* `err` `(string: <not success>)` - Error message.

---

## Get User's Information

| Method | Path                   |
| ------ | ---------------------- |
| `POST` | `users/getInformation` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `userInformation` `(json: <success>)`
  * `username` `(string)` - 使用者名稱
  * `email` `(string)` - 使用者Email
  * `phoneNumber` `(string)` - 使用者電話號碼

---

## Get All Materials

| Method | Path                       |
| ------ | -------------------------- |
| `POST` | `material/getAllMaterials` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `allMaterialInformation` `(array: <success>)`
  * `materialId` `(string)` - 原料Id
  * `name` `(string)` - 原料名稱
  * `amount` `(int)` - 原料數量

---

## Get Material History

| Method | Path                          |
| ------ | ----------------------------- |
| `POST` | `material/getMaterialHistory` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `materialId` `(string: <required>)` - 原料Id

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `materialInformation` `(array: <success>)` - 特定原料的購買記錄
  * `price` `(int)` - 購買價格
  * `amount` `(int)` - 購買數量
  * `cost` `(int)` - 購買總價
  * `time` `(string)` - 購買時間

---

## Add New Material

| Method | Path                      |
| ------ | ------------------------- |
| `POST` | `material/addNewMaterial` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `materialName` `(string: <required>)` - 原料名稱
* `materialPrice` `(int: <optional>)` - 原料價格
* `materialAmount` `(int: <optional>)` - 原料數量

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `message` `(string: <success>)` - "新增初始原料成功"

---

## Delete Material

| Method | Path                      |
| ------ | ------------------------- |
| `POST` | `material/deleteMaterial` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `materialId` `(string: <required>)` - 原料Id

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `message` `(string: <success>)` - "刪除原料成功"

---

## Update Material

| Method | Path                    |
| ------ | ----------------------- |
| `POST` | `material/updateAmount` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `materialId` `(string: <required>)` - 原料Id
* `amountChange` `(int: <required>)` - 原料更改的數量 (正數為增加, 負數為減少)
* `price` `(int: <required>)` - 若原料增加，則此值為新增原料的價格；若原料減少，則此值為原料的價格

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `message` `(string: <success>)` - "更新原料成功"

---

## Get All Products

| Method | Path                     |
| ------ | ------------------------ |
| `POST` | `product/getAllProducts` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `allProductInformation` `(array: <success>)`
  * `productId` `(string)` - 存貨Id
  * `name` `(string)` - 存貨名稱
  * `amount` `(int)` - 存貨數量
  * `price` `(int)` - 存貨價格
  * `materials` `(array: <success>)` - 存貨包含的原料
    * `materialId` `(string)` - 原料Id
    * `materialName` `(string)` - 原料名稱

---

## Get Product

| Method | Path                 |
| ------ | -------------------- |
| `POST` | `product/getProduct` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `productId` `(string: <required>)` - 存貨Id

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `productInformation` `(json: <success>)`
  * `productId` `(string)` - 存貨Id
  * `name` `(string)` - 存貨名稱
  * `amount` `(int)` - 存貨數量
  * `price` `(int)` - 存貨價格
  * `materials` `(array: <success>)` - 存貨包含的原料
    * `materialId` `(string)` - 原料Id
    * `materialName` `(string)` - 原料名稱

---

## Add New Product

| Method | Path                    |
| ------ | ----------------------- |
| `POST` | `product/addNewProduct` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `productName` `(string: <required>)` - 存貨名稱
* `productAmount` `(int: <required>)` - 存貨數量
* `productPrice` `(int: <required>)` - 存貨價格
* `materialIds` `(array: <optional>)` - 存貨包含的原料Id

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `message` `(string: <success>)` - "新增初始存貨成功"

---

## Delete Product

| Method | Path                    |
| ------ | ----------------------- |
| `POST` | `product/deleteProduct` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `productId` `(string: <required>)` - 存貨Id

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `message` `(string: <success>)` - "刪除存貨成功"

---

## Update Product

| Method | Path                   |
| ------ | ---------------------- |
| `POST` | `product/updateAmount` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `productId` `(string: <required>)` - 存貨Id
* `amountChange` `(int: <required>)` - 存貨更改的數量 (正數為增加, 負數為減少)

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `message` `(string: <success>)` - "更新存貨成功"

---

## Add New Tag

| Method | Path              |
| ------ | ----------------- |
| `POST` | `order/addNewTag` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `tagName` `(string: <required>)` - 標籤名稱

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `message` `(string: <success>)` - "新增標籤成功"
* `tagId` `(string: <success>)` - 標籤Id

---

## Get All Orders

| Method | Path                 |
| ------ | -------------------- |
| `POST` | `order/getAllOrders` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `allOrdersData` `(array: <success>)`
  * `orderId` `(string)` - 訂單Id
  * `createTime` `(string)` - 訂單建立時間
  * `totalPrice` `(int)` - 訂單總價格
  * `orderProducts` `(array: <success>)` - 訂單包含的存貨
    * `productId` `(string)` - 存貨Id
    * `productName` `(string)` - 存貨名稱
    * `productAmount` `(int)` - 存貨數量
    * `productPrice` `(int)` - 存貨價格
  * `tags` `(array: <success>)` - 訂單包含的標籤
    * `tagId` `(string)` - 標籤Id
    * `tagName` `(string)` - 標籤名稱

---

## Add New Order

| Method | Path                |
| ------ | ------------------- |
| `POST` | `order/addNewOrder` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `orderData` `(json: <required>)` - 訂單包含的存貨
  * `productId` `(string: <key>)` - 存貨Id
  * `productAmount` `(int: <value>)` - 存貨數量
* `totalPrice` `(int: <required>)` - 訂單總價格
* `tagIds` `(array: <required>)` - 訂單包含的標籤Id

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `message` `(string: <success>)` - "新增訂單成功"

---

## Delete Order

| Method | Path                |
| ------ | ------------------- |
| `POST` | `order/deleteOrder` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `orderId` `(string: <required>)` - 訂單Id

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `message` `(string: <success>)` - "刪除訂單成功"

---

## Update Order

| Method | Path                |
| ------ | ------------------- |
| `POST` | `order/updateOrder` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `orderId` `(string: <required>)` - 訂單Id
* `orderData` `(json: <required>)` - 訂單包含的存貨
  * `productId` `(string: <key>)` - 存貨Id
  * `productAmount` `(int: <value>)` - 存貨數量
* `totalPrice` `(int: <required>)` - 訂單總價格
* `tagIds` `(array: <required>)` - 訂單包含的標籤Id

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `message` `(string: <success>)` - "更新訂單成功"

---

## Get All Employee

| Method | Path                      |
| ------ | ------------------------- |
| `POST` | `schedule/getAllEmployee` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `allEmployee` `(array: <success>)` - 員工資料
  * `employeeId` `(string)` - 員工Id
  * `employeeName` `(string)` - 員工名稱
  * `employeeUnitSalary` `(int)` - 員工時薪
  * `emoloyeeWorkingHours` `(int)` - 員工當月工作時數
  * `employeeTotalSalary` `(int)` - 員工當月總薪水

---

## Add New Employee

| Method | Path                      |
| ------ | ------------------------- |
| `POST` | `schedule/addNewEmployee` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `employeeName` `(string: <required>)` - 員工名稱
* `employeeUnitSalary` `(int: <optional>)` - 員工時薪

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `message` `(string: <success>)` - "新增員工成功"

---

## Delete Employee

| Method | Path                      |
| ------ | ------------------------- |
| `POST` | `schedule/deleteEmployee` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `employeeId` `(string: <required>)` - 員工Id

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `message` `(string: <success>)` - "刪除員工成功"

---

## Update Employee

| Method | Path                      |
| ------ | ------------------------- |
| `POST` | `schedule/updateEmployee` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `employeeId` `(string: <required>)` - 員工Id
* `employeeName` `(string: <required>)` - 員工名稱
* `employeeUnitSalary` `(int: <optional>)` - 員工時薪

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `message` `(string: <success>)` - "更新員工成功"

---

## Get All Timeblock

| Method | Path                       |
| ------ | -------------------------- |
| `POST` | `schedule/getAllTimeblock` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `allTimeblock` `(array: <success>)` - 時段資料
  * `timeblockId` `(string)` - 時段Id
  * `employeeId` `(string)` - 員工Id
  * `employeeName` `(string)` - 員工名稱
  * `startTime` `(string)` - 時段開始時間
  * `endTime` `(string)` - 時段結束時間

---

## Add New Timeblock

| Method | Path                       |
| ------ | -------------------------- |
| `POST` | `schedule/addNewTimeblock` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `employeeId` `(string: <required>)` - 員工Id
* `startTime` `(string: <required>)` - 時段開始時間
* `endTime` `(string: <required>)` - 時段結束時間

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `message` `(string: <success>)` - "新增時段成功"
* `timeblockId` `(string: <success>)` - 時段Id

---

## Delete Timeblock

| Method | Path                       |
| ------ | -------------------------- |
| `POST` | `schedule/deleteTimeblock` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `timeblockId` `(string: <required>)` - 時段Id

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `message` `(string: <success>)` - "刪除時段成功"

---

## Update Timeblock

| Method | Path                       |
| ------ | -------------------------- |
| `POST` | `schedule/updateTimeblock` |

### Parameters

* `userId` `(string: <required>)` - 使用者Id
* `timeblockId` `(string: <required>)` - 時段Id
* `employeeId` `(string: <required>)` - 員工Id
* `employeeName` `(string: <required>)` - 員工名稱
* `startTime` `(string: <required>)` - 時段開始時間
* `endTime` `(string: <required>)` - 時段結束時間

### Responses

* `success` `(bool)` - True/False.
* `err` `(string: <not success>)` - Error message.
* `message` `(string: <success>)` - "更新時段成功"

