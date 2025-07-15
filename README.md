# 🧪 ResReq Postman Test Collection

This project contains a comprehensive Postman test suite for validating various endpoints of the [ReqRes API](https://reqres.in/), a free-to-use RESTful API for testing and prototyping.

## 🔍 Overview

The collection is divided into two main folders:

- **✅ Passed Requests** – Valid test scenarios such as:
  - Listing users
  - Listing a single user
  - Listing resources
  - Delayed responses

- **❌ Failed Requests** – Intended to test edge/error cases like:
  - Creating a user with missing data
  - Updating non-existent users
  - Failed registrations or logins

Each request is accompanied by automated test scripts written in JavaScript using the [Postman Sandbox API](https://learning.postman.com/docs/writing-scripts/script-references/test-examples/).

---

## ⚙️ Environment Setup

### 📄 Environment: `ReqRes`
This environment sets global variables to make requests dynamic and reusable:

| Key           | Value       | Description                      |
|---------------|-------------|----------------------------------|
| `base_url`    | `reqres.in` | Base API domain                  |
| `userID`      | *(random)*  | Set dynamically for user lookup |
| `resourceName`| *(set by tests)* | Used in resource validation tests |

> ✅ Be sure to select the `ReqRes` environment before running the collection in Postman.

---

## 🚀 How to Use

### ✅ 1. Import into Postman

- Go to **Postman > Import**
- Import both:
  - `ReqRes.postman_collection.json`
  - `ReqRes.postman_environment.json`

### ✅ 2. Select the Environment

- On the top-right in Postman, select the `ReqRes` environment from the dropdown.

### ✅ 3. Run the Collection

You can run individual requests or the entire collection via:
- **Collection Runner**: for full regression
- **Newman (CLI)**: for CI integration

---

## 🧪 Example Test Logic

Some requests contain multiple test assertions, such as:

```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response time is less than 1 second", function(){
    if (pm.info.requestName !== "Delayed Response") {
        pm.expect(pm.response.responseTime).to.be.below(1000);
    }
});


