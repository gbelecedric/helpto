# helpto

```python

from django.db import models
from django.contrib.auth.models import User

from django.db.models.signals import post_save
from django.dispatch import receiver


# Create your models here.

class Utilisateur(models.Model):
    
    user = models.OneToOneField(User, on_delete=models.CASCADE, related_name='profil_user')  
    picture = models.ImageField(upload_to='images/avatar/',null=True,blank=True)
    date_add =  models.DateTimeField(auto_now_add=True)
    date_update =  models.DateTimeField(auto_now=True)
    solde = models.PositiveIntegerField(default="0")

class OperationType(models.Model):
    
    libelle = models.CharField(max_length=200, null=True,blank=True)

    class Meta:

        verbose_name = 'OperationType'
        verbose_name_plural = 'OperationTypes'
    
    def __str__(self):
        return self.libelle
        

class Transactions(models.Model):
    
    utilisateur = models.ForeignKey(Utilisateur, on_delete=models.CASCADE,related_name='user_transaction',) 
    operation = models.ForeignKey(OperationType, on_delete=models.CASCADE,related_name='operation_transaction',) 
    date_add =  models.DateTimeField(auto_now_add=True)
    date_update =  models.DateTimeField(auto_now=True)

    class Meta:

        verbose_name = 'Transactions'
        verbose_name_plural = 'Transactionss'
    
    def __str__(self):
        return self.utilisateur.user.username

    




```
