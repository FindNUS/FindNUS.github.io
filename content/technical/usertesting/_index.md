---
title: "User Testing"
weight: 1
# geekdocFlatSection: false
# geekdocToc: 6
# geekdocHidden: false
---
The testing of the application can be broken down into functional and 
non-functional tests

<!-- omit in toc -->
## Table of Contents
- [Functional Testing](#functional-testing)
  - [Unit and Integration Testing](#unit-and-integration-testing)
- [Non-functional Testing](#non-functional-testing)
  - [Usability Testing](#usability-testing)
  - [Documentation Testing](#documentation-testing)


# Functional Testing

## Unit and Integration Testing

For frontend, we perform unit and integration testing with Jest and React 
Testing Library. For backend, unit testing is conducted with golang’s built-in 
testing function: `go test ..`, while integration testing is deployed to the 
User Acceptance Testing backend. For more information, 
[click here](../unittesting/)

<div align="right"><a href="#table-of-contents">Back to top</a></div>

# Non-functional Testing

## Usability Testing

To perform usability testing, the tester should to complete the following tasks

| Task            | Todo                                                                                                                                                                                                                               | Expected Result                                                                                                                                                                           |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Search          | Search for the item "iPhone 13" and view it                                                                                                                                                                                        | User should obtain the following item<br>![iPhone 13](https://i.imgur.com/G4mvbWz.png)                                                                                                    |
| Peek            | View recently uploaded items                                                                                                                                                                                                       | User should minimally see these items<br>![Peek Results](https://i.imgur.com/H6DmAri.png?1)                                                                                               |
| Filter          | Filter recent items with the category "Electronics"                                                                                                                                                                                | User should minimally see this item<br>![Filter Result](https://i.imgur.com/1afr6ug.png)                                                                                                  |
| Submit an item  | Submit a found item of your choice (image is optional)                                                                                                                                                                             | User should see their uploaded item (Possibly requires refresh after redirect)                                                                                                            |
| Login           | Attempt to login using either their own mobile number, an international phone number from [this page](https://receive-sms-free.cc/) or the following test account:<br>__Phone Number:__ +6511111111 (no spaces)<br>__OTP:__ 111111 | For the test account, user will see the following information:<br>![Test account dashboard](https://i.imgur.com/daKQh6m.png)<br>For other accounts, a different user ID will be displayed |
| Dashboard Items | View items uploaded with the test account above                                                                                                                                                                                    | User should minimally see this item<br>![Dashboard items](https://i.imgur.com/3LdHvb8.png)                                                                                                |
| Logout          | Attempt to logout of the application                                                                                                                                                                                               | Redirected to home page with login option                                                                                                                                                 |

<div align="right"><a href="#table-of-contents">Back to top</a></div>

## Documentation Testing

A sample of the API documentation can be found [here](../../swe/apisample/), 
and the deployment can be accessed at https://findnus.herokuapp.com/

__Search Query Example__

Refer to [`GET` /search](../../swe/apisample/#get-search) for more details.

To perform a search query for the item "Airpods", you may perform a `GET` 
request at the `/search` endpoint with the following URL: 
<a href="https://findnus.herokuapp.com/search?query=Airpods" 
target="_blank" 
rel="noopener">
https:<span>//</span>findnus.herokuapp.com/search?query=Airpods
</a>
You should expect to receive the following response:

```json
[
    {
        "Id":"62b82df7a5d9182afd9665a0",
        "Name":"Airpods",
        "Date":"2022-05-18T00:00:00Z",
        "Location":"UTown Bus Stop",
        "Category":"Electronics",
        "Item_details":"Please call me if found,
         thank you!!",
        "Image_url":"https://i.imgur.com/c5MuKsu.jpg"
    }
]
```

Which is equivalent to the following item

![Airpods](https://i.imgur.com/E5kWOph.png)

<div align="right"><a href="#table-of-contents">Back to top</a></div>
