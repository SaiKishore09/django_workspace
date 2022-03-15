# Django Coding Challenge

**Please make sure to go through the below details before cloning the repository**

**Goal**: REST API development, as per the below details

**Development of following items**
- **Registration API** with User Name, Email and Passowrd
- **Login API with Email** and Passowrd
- **Users Listing API** to get List of Names & Email
- **Profile Update API** to update the profile details like Name, Designation, Profile Picture and Team

**Scope of work**
- Create REST APIs for the below user journey
    - User should be able to register with Name, Email, Password.
    - Once the User is registered, the User should be able to Login with the same email and password.
    - Once the user is Logged in, the user should be able to list all the users present on the platform.
    - User list should contain the name and email address of the users.
- Get user listing API should be authenticated against the logged in users and should throw an error if it's not authenticated.
- Profile Update API where user can update Name,  Designation, Profile Picture and Team, This also will be an authenticated API
    - Proifle Picture - User will upload the profile picture this can be either through s3 bucket or local machine
    - Team - will be multi select from the predifined list provided below 
        - Development
        - Product
        - Design
        - Human Resource
- Database you can use MySQL / PostgreSQL.
- No need to host the APIs, You can directly submit the pull request against this repository and your code will be reviewed.


> :warning: [Designs Link](https://www.figma.com/file/2hbi9TlIZdxBB6jycyNWws?node-id=0:1#122675486) - This URL is only for the visualization of the flow and Only API development is required.


**Steps to follow to submit your code**
1. Fork the repository
2. Make your changes 
3. Submit the **Pull Request** from the forked repository 


**Please note: git push on this repository is not allowed and only pull requests (PRs) from the forked repositories are allowed**
 
Once you have completed the development, Please raise the pull request from your forked repository, and your work will be reviewed against:
- **Developed APIs & Models**
- **Coding Standards**
- **Readability & Reusability of code**
- **Code Quality and Size**

_This repository is meant to facilitate the interview process @Designstring and only referred candidates for the interview process are requested to access_

Happy Coding!!!

------"models"------
from django.db import models

class users(models.Model):
    name=models.CharField(max_length=10)
    email=models.IntegerField()

    def __str__(self):
        return self.name

------'"admin"--------

from django.contrib import admin
from . models import users

admin.site.register(users)


---------"serializers"--------

from django.contrib import admin
from . models import users

admin.site.register(users)

---------"views"----------

from django.shortcuts import render
from django.http import HttpResponse
from django.shortcuts import get_object_or_404
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status
from . models import users
from . serializers import userserializers

class userlist(APIView):

    def get(self,request):
        user1=users.objects.all()
        serializer=userserializers(user1,many=True)
        return Response(serializer.data)

------------"urls"-----

from django.contrib import admin
from django.urls import path
from rest_framework.urlpatterns import format_suffix_patterns
from social import views


urlpatterns = [
    path('admin/', admin.site.urls),
    path('users/', views.userlist.as_view()),
]




