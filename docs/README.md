# FONA: Food Nutrition Assistant

> Android-based application with a machine learning model to calculate how much nutrition the user needs and give a recommendation about what foods with nutrition that is suitable for the user.

---

## Documentation URL
> https://bit.ly/fona-documentation

---

## FONA Github
> https://github.com/FONA-Food-Nutrition-Assistant

---

## Table of Contents
- [FONA: Food Nutrition Assistant](#fona-food-nutrition-assistant)
- [Documentation URL](#documentation-url)
- [FONA Github](#fona-github)
- [Endpoint](#endpoint)
- [User Service](#user-service)
   - [Store User Data](#store-user-data)
   - [Update User Data](#update-user-data)
   - [Get User Data](#get-user-data)
- [Food Service](#food-service)
   - [Get List of Foods](#get-list-of-foods)
   - [Get Food Details](#get-food-details)
   - [Get List of Nutrition](#get-list-of-nutrition)
   - [Get List of Allergy](#get-list-of-allergy)
   - [Home (Get All User Recorded Foods, Recorded Water, Daily Analysis, and Food Suggestion)](#home-get-all-user-recorded-foods-recorded-water-daily-analysis-and-food-suggestion)
   - [Store User Recorded Foods](#store-user-recorded-foods)
   - [Update User Recorded Foods](#update-user-recorded-foods)
   - [Store User Recorded Waters](#store-user-recorded-waters)
   - [Update User Recorded Waters](#update-user-recorded-waters)
- [Identification Service](#identification-service)
   - [Identify Food Nutrition](#identify-food-nutrition)

---

## Endpoint

- BASE_URL
  - https://gateway-service-m22xk2kynq-as.a.run.app/gateway/v1

---

## User Service

- Endpoint
  - `[BASE_URL]/us/[API_URL]`

### Store User's Data

- URL
  - `/user`
- Method
  - `POST`
- Request Headers
  - `Authorization` as `Bearer`, value of id token from firebase authentication
- Request Body
  - `height` as `int`, value in cm
  - `weight` as `int`, value in kg
  - `gender` as `Laki-laki | Perempuan`
  - `date_of_birth` as `YYYY-MM-DD`
  - `activity` as `Tidak Aktif | Sedikit Aktif | Cukup Aktif | Sangat Aktif | Ekstra Aktif`
  - `allergies` as `Array of int`, value of allergy’s id
- Response
  ```json
  {
    "height": "int",
    "weight": "int",
    "gender": "Laki-laki | Perempuan",
    "date_of_birth": "YYYY-MM-DD",
    "activity": "Tidak Aktif | Sedikit Aktif | Cukup Aktif | Sangat Aktif | Ekstra Aktif",
    "allergies": "[Array of int]"
  }
  ```

### Update User's Data

- URL
  - `/user`
- Method
  - `PUT`
- Request Headers
  - `Authorization` as `Bearer`, value of id token from firebase authentication
- Request Body
  - Optional
    - `height` as `int`, value in cm
    - `weight` as `int`, value in kg
    - `gender` as `Male | Female`
    - `date_of_birth` as `YYYY-MM-DD`
    - `activity` as `Tidak Aktif | Sedikit Aktif | Cukup Aktif | Sangat Aktif | Ekstra Aktif`
    - `allergies` as `Array of int`, value of allergy’s id
- Response

```json
{
  "status": 200,
  "method": "PUT",
  "message": "Successfully update data",
  "data": {
    "uid": "p5LHOtRdUcM7Iyj7oTRHM6z3mhr1",
    "height": 178,
    "weight": 100,
    "date_of_birth": "2002-06-05",
    "activity": "Ekstra Aktif",
    "gender": "Laki-laki",
    "created_at": "2023-12-07T19:13:36.718Z",
    "updated_at": "2023-12-11T12:02:07.581Z",
    "allergies": [
      {
        "id": 5,
        "name": "Telur"
      },
      {
        "id": 6,
        "name": "Udang"
      }
    ]
  }
}
```

### Get User's Data

- URL
  - `/user`
- Method
  - `GET`
- Request Headers
  - `Authorization` as `Bearer`, value of id token from firebase authentication

Response

```json
{
  "status": 200,
  "method": "GET",
  "message": "Successfully get list of data",
  "data": {
    "uid": "p5LHOtRdUcM7Iyj7oTRHM6z3mhr1",
    "height": 178,
    "weight": 102,
    "date_of_birth": "2002-06-05T00:00:00.000Z",
    "activity": "Extremely Active",
    "gender": "Male",
    "created_at": "2023-12-07T19:13:36.718Z",
    "updated_at": "2023-12-08T06:51:55.144Z",
    "age": 21,
    "bmi": 32.19,
    "tdee": 3861.75,
    "allergies": [
      {
        "id": 5,
        "name": "Telur"
      },
      {
        "id": 6,
        "name": "Udang"
      }
    ]
  }
}
```

---

## Food Service

- Endpoint
  - `[BASE_URL]/fs/[API_URL]`

### Get List of Foods

- URL
  - `/food`
- Method
  - `GET`
- Request Headers
  - `Authorization` as `Bearer`, value of id token from firebase authentication
- Request Params
  - Optional
    - `page` as `int`, default is 1
    - `limit` as `int`, default is 0 (display all data)
    - `id` as `int`, value of food’s id, can be multiple using (,) e.g. `1,2,3`
    - `search` as `string`, keyword of food name
    - `sort` as `id | name`
    - `order` as `ASC | DESC`
- Response

```json
{
  "status": 200,
  "method": "GET",
  "message": "Successfully get list of data",
  "data": [
    {
      "id": 7,
      "name": "Ayam Goreng",
      "created_at": "2023-12-07T20:18:43.804Z",
      "updated_at": "2023-12-07T20:18:43.835Z"
    },
    {
      "id": 8,
      "name": "Ayam Bakar",
      "created_at": "2023-12-07T20:18:43.804Z",
      "updated_at": "2023-12-07T20:18:43.835Z"
    },
    {
      "id": 27,
      "name": "Opor Ayam",
      "created_at": "2023-12-07T20:18:43.804Z",
      "updated_at": "2023-12-07T20:18:43.835Z"
    }
  ]
}
```

### Retrieve a Food's Details

- URL
  - `/food/detail`
- Method
  - `GET`
- Request Headers
  - `Authorization` as `Bearer`, value of id token from firebase authentication
- Request Params
  - Optional
    - `page` as `int`, default is 1
    - `limit` as `int`, default is 0 (display all data)
    - `id` as `int`, value of food’s id, can be multiple using (,) e.g. `1,2,3`
    - `search` as `string`, keyword of food name, can be multiple using (,) e.g. `ayam,kangkung`
    - `sort` as `id | name`
    - `order` as `ASC | DESC`
- Response

```json
{
  "status": 200,
  "method": "GET",
  "message": "Successfully get list of data",
  "data": [
    {
      "id": 12,
      "name": "Kangkung Tumis",
      "is_user_allergy": false,
      "nutritions": [
        {
          "id": 354,
          "food_id": 12,
          "serving_size": "100 gram",
          "cals": 106,
          "carbos": 4.31,
          "proteins": 2.76,
          "fibers": 1.8,
          "fats": 9.4,
          "glucoses": 0.55,
          "sodiums": 0.414,
          "caliums": 0.456,
          "created_at": "2023-12-08T03:19:34.596Z",
          "updated_at": "2023-12-09T05:49:04.322Z"
        },
        {
          "id": 353,
          "food_id": 12,
          "serving_size": "1 porsi (85 gram)",
          "cals": 98,
          "carbos": 3.99,
          "proteins": 2.56,
          "fibers": 1.7,
          "fats": 8.71,
          "glucoses": 0.51,
          "sodiums": 0.384,
          "caliums": 0.422,
          "created_at": "2023-12-08T03:19:34.596Z",
          "updated_at": "2023-12-09T05:49:04.322Z"
        }
      ]
    }
  ]
}
```

### Retrieve the list of nutrition for foods.

- URL
  - `/food/nutrition`
- Method
  - `GET`
- Request Headers
  - `Authorization` as `Bearer`, value of id token from firebase authentication
- Request Params
  - Optional
    - `page` as `int`, default is 1
    - `limit` as `int`, default is 0 (display all data)
    - `id` as `int`, value of nutrition’s id, can be multiple using (,) e.g. `1,2,3`
    - `food_id` as `int`, value of food’s id, can be multiple using (,) e.g. `1,2,3`
    - `order` as `ASC | DESC`
- Response

```json
{
  "status": 200,
  "method": "GET",
  "message": "Successfully get list of data",
  "data": [
    {
      "id": 332,
      "food_id": 1,
      "serving_size": "100 gram",
      "cals": 129,
      "carbos": 27.9,
      "proteins": 2.66,
      "fibers": 0,
      "fats": 0.28,
      "glucoses": 0,
      "sodiums": 0.365,
      "caliums": 0.035,
      "created_at": "2023-12-08T03:19:34.596Z",
      "updated_at": "2023-12-08T03:19:34.614Z"
    },
    {
      "id": 333,
      "food_id": 1,
      "serving_size": "1 porsi (105 gram)",
      "cals": 135,
      "carbos": 29.3,
      "proteins": 2.79,
      "fibers": 0.4,
      "fats": 0.29,
      "glucoses": 0.05,
      "sodiums": 0.383,
      "caliums": 0.037,
      "created_at": "2023-12-08T03:19:34.596Z",
      "updated_at": "2023-12-08T03:19:34.614Z"
    }
  ]
}
```

### Retrieve the List of Allergies

- URL
  - `/allergy`
- Method
  - `GET`
- Request Headers
  - `Authorization` as `Bearer`, value of id token from firebase authentication
- Request Params
  - Optional
    - `page` as `int`, default is 1
    - `limit` as `int`, default is 0 (display all data)
    - `id` as `int`, value of nutrition’s id, can be multiple using (,) e.g. `1,2,3`
    - `sort` as `id | name`
    - `order` as `ASC | DESC`
- Response

```json
{
  "status": 200,
  "method": "GET",
  "message": "Successfully get list of data",
  "data": [
    {
      "id": 5,
      "name": "Telur"
    },
    {
      "id": 6,
      "name": "Udang"
    },
    {
      "id": 7,
      "name": "Ikan"
    }
  ]
}
```

### Retrieve the User's Recorded Consumed Foods, Consumed Water, Daily Analysis, and Food Suggestions for the User

- URL
  - `/home`
- Method
  - `GET`
- Request Headers
  - `Authorization` as `Bearer`, value of id token from firebase authentication
- Request Params
  - Required
    - `date` as `YYYY-MM-DD`
- Response

```json
{
  "status": 200,
  "method": "GET",
  "message": "Successfully get list of data",
  "data": {
    "calorie_intake": {
      "lowest_breakfast_intake": 477,
      "highest_breakfast_intake": 611,
      "lowest_lunch_intake": 561,
      "highest_lunch_intake": 695,
      "lowest_dinner_intake": 393,
      "highest_dinner_intake": 611
    },
    "daily_needs": {
      "TDEE": 1674,
      "proteins": 167.4,
      "fats": 334.8,
      "carbos": 753.3
    },
    "daily_analysis": {
      "total_cals": 2199,
      "total_carbos": 257.44,
      "total_proteins": 88.02,
      "total_fibers": 17.65,
      "total_fats": 91.06,
      "total_glucoses": 8.68,
      "total_sodiums": 4.16,
      "total_caliums": 3.42
    },
    "record_foods": {
      "breakfast": [
        {
          "food_id": 1,
          "nutrition_id": 333,
          "name": "Nasi Putih",
          "serving_size": "1 porsi (105 gram)",
          "quantity": 2,
          "total_cals": 270,
          "total_carbos": 58.6,
          "total_proteins": 5.58,
          "total_fats": 0.58,
          "total_fibers": 0.8,
          "total_caliums": 0.07,
          "total_sodiums": 0.77,
          "total_glucoses": 0.1
        },
        {
          "food_id": 12,
          "nutrition_id": 353,
          "name": "Kangkung Tumis",
          "serving_size": "1 porsi (85 gram)",
          "quantity": 1,
          "total_cals": 98,
          "total_carbos": 3.99,
          "total_proteins": 2.56,
          "total_fats": 8.71,
          "total_fibers": 1.7,
          "total_caliums": 0.42,
          "total_sodiums": 0.38,
          "total_glucoses": 0.51
        },
        {
          "food_id": 26,
          "nutrition_id": 382,
          "name": "Martabak Telur",
          "serving_size": "1 porsi (110 gram)",
          "quantity": 2,
          "total_cals": 406,
          "total_carbos": 40.76,
          "total_proteins": 21.78,
          "total_fats": 16.9,
          "total_fibers": 2.8,
          "total_caliums": 0.46,
          "total_sodiums": 0.3,
          "total_glucoses": 2.06
        }
      ],
      "lunch": [
        {
          "food_id": 1,
          "nutrition_id": 333,
          "name": "Nasi Putih",
          "serving_size": "1 porsi (105 gram)",
          "quantity": 1,
          "total_cals": 135,
          "total_carbos": 29.3,
          "total_proteins": 2.79,
          "total_fats": 0.29,
          "total_fibers": 0.4,
          "total_caliums": 0.04,
          "total_sodiums": 0.38,
          "total_glucoses": 0.05
        },
        {
          "food_id": 12,
          "nutrition_id": 353,
          "name": "Kangkung Tumis",
          "serving_size": "1 porsi (85 gram)",
          "quantity": 2,
          "total_cals": 196,
          "total_carbos": 7.98,
          "total_proteins": 5.12,
          "total_fats": 17.42,
          "total_fibers": 3.4,
          "total_caliums": 0.84,
          "total_sodiums": 0.77,
          "total_glucoses": 1.02
        },
        {
          "food_id": 26,
          "nutrition_id": 382,
          "name": "Martabak Telur",
          "serving_size": "1 porsi (110 gram)",
          "quantity": 2,
          "total_cals": 406,
          "total_carbos": 40.76,
          "total_proteins": 21.78,
          "total_fats": 16.9,
          "total_fibers": 2.8,
          "total_caliums": 0.46,
          "total_sodiums": 0.3,
          "total_glucoses": 2.06
        }
      ],
      "dinner": [
        {
          "food_id": 1,
          "nutrition_id": 333,
          "name": "Nasi Putih",
          "serving_size": "1 porsi (105 gram)",
          "quantity": 1,
          "total_cals": 135,
          "total_carbos": 29.3,
          "total_proteins": 2.79,
          "total_fats": 0.29,
          "total_fibers": 0.4,
          "total_caliums": 0.04,
          "total_sodiums": 0.38,
          "total_glucoses": 0.05
        },
        {
          "food_id": 12,
          "nutrition_id": 353,
          "name": "Kangkung Tumis",
          "serving_size": "1 porsi (85 gram)",
          "quantity": 1.5,
          "total_cals": 147,
          "total_carbos": 5.99,
          "total_proteins": 3.84,
          "total_fats": 13.07,
          "total_fibers": 2.55,
          "total_caliums": 0.63,
          "total_sodiums": 0.58,
          "total_glucoses": 0.77
        },
        {
          "food_id": 26,
          "nutrition_id": 382,
          "name": "Martabak Telur",
          "serving_size": "1 porsi (110 gram)",
          "quantity": 2,
          "total_cals": 406,
          "total_carbos": 40.76,
          "total_proteins": 21.78,
          "total_fats": 16.9,
          "total_fibers": 2.8,
          "total_caliums": 0.46,
          "total_sodiums": 0.3,
          "total_glucoses": 2.06
        }
      ]
    },
    "record_water": 1,
    "food_suggestion": {
      "breakfast": {
        "id": 2,
        "name": "Paket Gorengan",
        "image_url": "https://storage.googleapis.com/fona-packets/paket_gorengan.png",
        "total_cals": 525,
        "foods": [
          {
            "id": 1,
            "name": "Nasi Putih",
            "cals": 525
          },
          {
            "id": 22,
            "name": "Bakwan",
            "cals": 525
          },
          {
            "id": 23,
            "name": "Ikan Goreng",
            "cals": 525
          }
        ]
      },
      "lunch": {
        "id": 19,
        "name": "Mie Goreng Polos",
        "image_url": "https://storage.googleapis.com/fona-packets/paket_mie_goreng_polos.png",
        "total_cals": 426,
        "foods": [
          {
            "id": 4,
            "name": "Mie Goreng",
            "cals": 426
          },
          {
            "id": 10,
            "name": "Telur",
            "cals": 426
          },
          {
            "id": 25,
            "name": "Kerupuk",
            "cals": 426
          }
        ]
      },
      "dinner": {
        "id": 50,
        "name": "Paket Bakso Malang",
        "image_url": "https://storage.googleapis.com/fona-packets/paket_bakso_malang.png",
        "total_cals": 542,
        "foods": [
          {
            "id": 21,
            "name": "Bakso",
            "cals": 542
          },
          {
            "id": 22,
            "name": "Bakwan",
            "cals": 542
          },
          {
            "id": 9,
            "name": "Tahu",
            "cals": 542
          },
          {
            "id": 3,
            "name": "Bihun Goreng",
            "cals": 542
          }
        ]
      }
    }
  }
}
```

### Store the Foods Consumed by the User

- URL
  - `/food`
- Method
  - `POST`
- Request Headers
  - `Authorization` as `Bearer`, value of id token from firebase authentication
- Request Body
  - Required
    - `foods` as `Array of Object`, value of nutrition’s id and quantity
      ```json
      {
        "nutrition_id": 400,
        "quantity": 1
      }
      ```
    - `meal_time` as `Sarapan| Makan Siang | Makan Malam`
    - `date` as `YYYY-MM-DD`

```json
{
  "status": 200,
  "method": "POST",
  "message": "Successfully create data",
  "data": {
    "is_foods_contain_allergies": false,
    "foods_contain_allergies": [],
    "data": [
      {
        "user_id": "sElvAQJsevR1s68eE2z5wC4kdc22",
        "nutrition_id": 400,
        "quantity": 1,
        "date": "2023-09-03T00:00:00.000Z",
        "meal_time": "Sarapan",
        "id": 434
      },
      {
        "user_id": "sElvAQJsevR1s68eE2z5wC4kdc22",
        "nutrition_id": 376,
        "quantity": 1,
        "date": "2023-09-03T00:00:00.000Z",
        "meal_time": "Sarapan",
        "id": 435
      }
    ]
  }
}
```

### Update the Foods Consumed by the User

- URL
  - `/food`
- Method
  - `PUT`
- Request Headers
  - `Authorization` as `Bearer`, value of id token from firebase authentication
- Request Body
  - Required
    - `foods` as `Array of Object`, value of nutrition’s id and quantity
    ```json
    {
      "nutrition_id": 400,
      "quantity": 1
    }
    ```
    - `meal_time` as `Sarapan| Makan Siang | Makan Malam`
    - `date` as `YYYY-MM-DD`

```json
{
  "status": 200,
  "method": "PUT",
  "message": "Successfully update data",
  "data": {
    "is_foods_contain_allergies": false,
    "foods_contain_allergies": [],
    "data": [
      {
        "user_id": "sElvAQJsevR1s68eE2z5wC4kdc22",
        "nutrition_id": 400,
        "quantity": 1,
        "date": "2023-09-04T00:00:00.000Z",
        "meal_time": "Sarapan"
      },
      {
        "user_id": "sElvAQJsevR1s68eE2z5wC4kdc22",
        "nutrition_id": 376,
        "quantity": 1,
        "date": "2023-09-04T00:00:00.000Z",
        "meal_time": "Sarapan"
      }
    ]
  }
}
```

### Store the Water Consumed by the User

- URL
  - `/water`
- Method
  - `POST`
- Request Headers
  - `Authorization` as `Bearer`, value of id token from firebase authentication
- Request Body
  - Required
    - `number_as_cups` as int, value of user water consumption
    - `date` as `YYYY-MM-DD`
- Response

```json
{
  "status": 200,
  "method": "POST",
  "message": "Successfully create data",
  "data": []
}
```

### Update the Water Consumed by the User

- URL
  - `/water`
- Method - `PUT`
  Request Headers - `Authorization` as `Bearer`, value of id token from firebase authentication
- Request Body
  - Required
    - `number_as_cups` as int, value of user water consumption
    - `date` as `YYYY-MM-DD`
- Response

```json
{
  "status": 200,
  "method": "PUT",
  "message": "Successfully update data",
  "data": {
    "id": 20,
    "user_id": "sElvAQJsevR1s68eE2z5wC4kdc22",
    "number_of_cups": 10,
    "date": "2023-09-28T17:00:00.000Z",
    "created_at": "2023-12-12T23:55:52.898Z",
    "updated_at": "2023-12-12T23:55:52.898Z"
  }
}
```

---

## Identification Service

- Endpoint
  - `[BASE_URL]/is/[API_URL]`

### Identify Nutritional Information for Foods

- URL
  - `/identification/predict`
- Method
  - `POST`
- Request Headers
  - `Authorization` as `Bearer`, value of id token from firebase authentication
- Request Body as `multipart/form-data`
  - Required
    - `image` as `file/blob`, a photo taken by user that contains food
- Response

```json
{
    "status": 200,
    "method": "POST",
    "message": "Successfully get data",
    "data": [
        {
            "id": 8,
            "name": "Ayam Bakar",
            "is_user_allergy": false,
            "nutritions": [
                {
                    "id": 345,
                    "food_id": 8,
                    "serving_size": "100 gram",
                    "cals": 188,
                    "carbos": 0,
                    "proteins": 28.69,
                    "fibers": 0,
                    "fats": 7.35,
                    "glucoses": 0,
                    "sodiums": 0.409,
                    "caliums": 0.241,
                    "created_at": "2023-12-08T03:19:34.596Z",
                    "updated_at": "2023-12-08T03:19:34.614Z"
                },
                {
                    "id": 346,
                    "food_id": 8,
                    "serving_size": "1 potong",
                    "cals": 162,
                    "carbos": 0,
                    "proteins": 24.67,
                    "fibers": 0,
                    "fats": 6.32,
                    "glucoses": 0,
                    "sodiums": 0.351,
                    "caliums": 0.207,
                    "created_at": "2023-12-08T03:19:34.596Z",
                    "updated_at": "2023-12-08T03:19:34.614Z"
                }
            ]
        },
						.... (other data),
        {
            "id": 25,
            "name": "Kerupuk",
            "is_user_allergy": false,
            "nutritions": [
                {
                    "id": 379,
                    "food_id": 25,
                    "serving_size": "100 gram",
                    "cals": 432,
                    "carbos": 69.32,
                    "proteins": 5.51,
                    "fibers": 2.3,
                    "fats": 14.04,
                    "glucoses": 3.23,
                    "sodiums": 0.382,
                    "caliums": 0.062,
                    "created_at": "2023-12-08T03:19:34.596Z",
                    "updated_at": "2023-12-08T03:19:34.614Z"
                },
                {
                    "id": 380,
                    "food_id": 25,
                    "serving_size": "1 keping",
                    "cals": 65,
                    "carbos": 10.4,
                    "proteins": 0.83,
                    "fibers": 0.3,
                    "fats": 2.11,
                    "glucoses": 0.48,
                    "sodiums": 0.057,
                    "caliums": 0.009,
                    "created_at": "2023-12-08T03:19:34.596Z",
                    "updated_at": "2023-12-08T03:19:34.614Z"
                }
            ]
        }
    ]
}
```
