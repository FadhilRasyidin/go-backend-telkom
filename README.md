# Overview

---
I will be using yesterday's task admission as it has already implemented some fundamental ecommerce features

## Tasks

- [x] Buatlah API untuk menampilkan list produk seperti pada gambar dibawah ini. Pada API list produk juga bisa untuk menghandle search by product name
- [x] Buatlah API untuk menampilkan produk detail seperti gambar dibawah ini.
- [x] Buatlah API untuk menambah, mengubah dan menghapus produk (Create, Update, Delete)
- [x] Hanya authenticated user yang dapat mengakses API Create, Update, dan Delete produk, selain itu API bisa diakses oleh guest user
- [ ] Pada API Create Produk dan Update Produk harus dapat mengupload image produk ke minio. Pada kedua API ini disarankan menggunakan form data untuk request payloadnya
- [ ] Format penyimpanan di minio menggunakan <host-url>/<bucket-name>/<product-key-name>

### Plus Points

- [ ] Dapat menyimpan image di minio tanpa menggunakan temporary image
- [ ] Image yang disimpan diminio dapat diakses publik dan memenuhi kriteria diatas

#### How to Run

```bash
# You can start the project with below commands
docker-compose up -d
go run main.go
```

- **SIGNUP FUNCTION API CALL (POST REQUEST)**

http://localhost:8000/users/signup

```json
{
  "first_name": "fadhil",
  "last_name": "fadhil",
  "email": "fadhil@gmail.com",
  "password": "fadhilfadhil",
  "phone": "+4534545435"
}
```

Response :"Successfully Signed Up!!"

- **LOGIN FUNCTION API CALL (POST REQUEST)**

  http://localhost:8000/users/login

```json
{
  "email": "fadhil@gmail.com",
  "password": "fadhilfadhil"
}
```

response will be like this

```json
{
  "_id": "***********************",
  "first_name": "fadhil",
  "last_name": "fadhil",
  "password": "$2a$14$UIYjkTfnFnhg4qhIfhtYnuK9qsBQifPKgu/WPZAYBaaN17j0eTQZa",
  "email": "fadhil@gmail.com",
  "phone": "+4534545435",
  "token": "eyJc0Bwcm90b25vbWFpbC5jb20iLCJGaXJzdF9OYW1lIjoiam9zZXBoIiwiTGFzdF9OYW1lIjoiaGVybWlzIiwiVWlkIjoiNjE2MTRmNTM5ZjI5YmU5NDJiZDlkZjhlIiwiZXhwIjoxNjMzODUzNjUxfQ.NbcpVtPLJJqRF44OLwoanynoejsjdJb5_v2qB41SmB8",
  "Refresh_Token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJFbWFpbCI6IiIsIkZpcnLCJVaWQiOiIiLCJleHAiOjE2MzQzNzIwNTF9.ocpU8-0gCJsejmCeeEiL8DXhFcZsW7Z3OCN34HgIf2c",
  "created_at": "2022-04-09T08:14:11Z",
  "updtaed_at": "2022-04-09T08:14:11Z",
  "user_id": "61614f539f29be942bd9df8e",
  "usercart": [],
  "address": [],
  "orders": []
}
```

- **Admin add Product Function (POST REQUEST)**

  http://localhost:8000/admin/addproduct

```json
{
  "product_name": "Xiaomi Mi Band 2 Smartwatch",
  "price": 150000,
  "rating": 3,
  "image": "xia.jpg"
}
```

Response : "Successfully added our Product Admin!!"

- **View all the Products in db GET REQUEST**

  http://localhost:8000/users/productview

Response

```json
[
  {
    "Product_ID": "6153ff8edef2c3c0a02ae39a",
    "product_name": "xiaomimiband2smartwatch",
    "price": 15000,
    "rating": 3,
    "image": "xia.jpg"
  }
]
```

- **Search Product by regex function (GET REQUEST)**

defines the word search sorting
http://localhost:8000/users/search?name=al

response:

```json
[
  {
    "Product_ID": "6153ff8edef2c3c0a02ae39a",
    "product_name": "xiaomimiband2smartwatch",
    "price": 15000,
    "rating": 3,
    "image": "xia.jpg"
  }
]
```

- **Adding the Products to the Cart (GET REQUEST)**

  http://localhost:8000/addtocart?id=xxxproduct_idxxx&userID=xxxxxxuser_idxxxxxx

  Corresponding mongodb query

- **Removing Item From the Cart (GET REQUEST)**

  http://localhost:8000/addtocart?id=xxxxxxx&userID=xxxxxxxxxxxx

- **Listing the item in the users cart (GET REQUEST) and total price**

  http://localhost:8000/listcart?id=xxxxxxuser_idxxxxxxxxxx

- **Addding the Address (POST REQUEST)**

  http://localhost:8000/addadress?id=user_id**\*\***\***\*\***

  The Address array is limited to two values home and work address more than two address is not acceptable

```json
{
  "house_name": "kosan",
  "street_name": "perkici x",
  "city_name": "tangsel",
  "pin_code": "15222"
}
```

- **Editing the Home Address(PUT REQUEST)**

  http://localhost:8000/edithomeaddress?id=xxxxxxxxxxuser_idxxxxxxxxxxxxxxx

- **Editing the Work Address(PUT REQUEST)**

  http://localhost:8000/editworkaddress?id=xxxxxxxxxxuser_idxxxxxxxxxxxxxxx

- **Delete Addresses(GET REQUEST)**

  http://localhost:8000/deleteaddresses?id=xxxxxxxxxuser_idxxxxxxxxxxxxx

  delete both addresses

- **Cart Checkout Function and placing the order(GET REQUEST)**

  After placing the order the items have to be deleted from cart functonality added

  http://localhost:8000?id=xxuser_idxxx

- **Instantly Buying the Products(GET REQUEST)**
  http://localhost:8000?userid=xxuser_idxxx&pid=xxxxproduct_idxxxx
