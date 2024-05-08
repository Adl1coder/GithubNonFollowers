# GitHub Non-Followers Finder

Bu Python kodu, bir GitHub kullanıcısının takip ettiği kullanıcıları ve kendisini takip etmeyenleri bulur :D

## Nasıl Kullanılır

1. `find_non_followers` fonksiyonunu tanımlayan kod parçacığını alın.
2. Kendi GitHub kullanıcı adınızı ve kişisel erişim belirtecinizi (`github_username` ve `github_token` değişkenleri) kod parçacığına ekleyin.
3. Kodu çalıştırın ve kullanıcılarınızın sizi takip etmeyenlerini görün.

## Kullanılan Kütüphaneler

 [Requests](https://docs.python-requests.org/) kütüphanesi 

## Örnek Kod

```python
import requests

def find_non_followers(username, token):
    api_url = f"https://api.github.com/users/{username}/following"
    headers = {
        "Authorization": f"token {token}"
    }
    following_response = requests.get(api_url, headers=headers)
    following = [user['login'] for user in following_response.json()]

    followers_url = f"https://api.github.com/users/{username}/followers"
    followers_response = requests.get(followers_url, headers=headers)
    followers = [user['login'] for user in followers_response.json()]

    non_followers = [user for user in following if user not in followers]

    return non_followers

github_username = "YourUsername"
github_token = "YourToken"

non_followers = find_non_followers(github_username, github_token)

print("Users not following you back:")
for user in non_followers:
    print(user)
