import requests
import json

api_key = "f9c15e6710msh6557edc269cc09ap11e1ccjsndcdf7390ff2c"

headers = {
	"api_key": api_key,
	"X-RapidAPI-Host": "petstore109.p.rapidapi.com",
	"X-RapidAPI-Key": api_key
}

post_headers = {
	"content-type": "application/json",
	"api_key": "f9c15e6710msh6557edc269cc09ap11e1ccjsndcdf7390ff2c",
	"X-RapidAPI-Host": "petstore109.p.rapidapi.com",
	"X-RapidAPI-Key": "f9c15e6710msh6557edc269cc09ap11e1ccjsndcdf7390ff2c"
}

def get_user_by_name(headers, name):
    res = requests.get(f"https://petstore109.p.rapidapi.com/user/{name}", headers=headers)
    status = res.status_code
    result = res.text
    try:
        result = res.json()
    except:
        result = json.decoder.JSONDecodeError
    return status, result

def create_user(headers, id=0, name="", firstname="", lastname="", email="", password="", phone="", userStatus=0):

    data = {
        "id": id,
        "username": name,
        "firstName": firstname,
        "lastName": lastname,
        "email": email,
        "password": password,
        "phone": phone,
        "userStatus": userStatus
    }

    res = requests.post("https://petstore109.p.rapidapi.com/user", headers=headers, json=data)
    status = res.status_code
    result = res.text
    try:
        result = res.json()
    except:
        result = json.decoder.JSONDecodeError
    return status, result

def update_user(headers, id=0, name="", firstname="", lastname="", email="", password="", phone="", userStatus=0):

    data = {
        "id": id,
        "username": name,
        "firstName": firstname,
        "lastName": lastname,
        "email": email,
        "password": password,
        "phone": phone,
        "userStatus": userStatus
    }

    res = requests.put(f"https://petstore109.p.rapidapi.com/user/{name}", headers=headers, json=data)
    status = res.status_code
    result = res.text
    try:
        result = res.json()
    except:
        result = json.decoder.JSONDecodeError
    return status, result


def delete_user(headers, name: str):
    res = requests.delete(f"https://petstore109.p.rapidapi.com/user/{name}", headers=headers)
    status = res.status_code
    result = res.text
    try:
        result = res.json()
    except:
        result = json.decoder.JSONDecodeError
    return status, result

def test_positive_create_user():
    name = 'Albert'
    res = create_user(post_headers, name=name)
    status = res[0]
    assert status == 200

def test_positive_user_by_name():
    name = 'Albert'
    res = get_user_by_name(headers, name)
    status = res[0]
    assert status == 200

def test_negative_user_by_name():
    name = 'Puk_Puk'
    res = get_user_by_name(headers, name)
    status = res[0]
    assert status == 404

def test_positive_update_user():
    name = 'Albert'
    new_id = 41
    new_firstName = 'Einstein'
    res = update_user(post_headers, id=new_id, name=name, firstname=new_firstName)
    status = res[0]
    assert status == 200 and get_user_by_name(headers, name)[1]["id"] == new_id

def test_positive_delete_user():
    name = 'Albert'
    res = delete_user(headers, name)
    status = res[0]
    assert status == 200

def test_negative_delete_user():
    name = 'Srenk_Srenk'
    res = delete_user(headers, name)
    status = res[0]
    assert status == 404



print(create_user(post_headers, name=False))
print(update_user(post_headers, id=5, name="Roma"))
print(get_user_by_name(headers, "Roma"))
print(delete_user(headers, "Roma"))
print(get_user_by_name(headers, "Roma"))
