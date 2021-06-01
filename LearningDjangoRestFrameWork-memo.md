# DjangoRestFrameWorkメモ  

以下コマンドでインストール  
```terminal
pip install djangorestframework
```

settings.py
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'rest_framework', 
]
```

djangoのviewイコールdjangorestframeworkのapiviewの認識  
また、drfを使ってモデルをjsonやxml形式などにうまく変換してくれるのがserializer  

viewの中では以下が必須  
views.py  
```python
class SampleAPI(APIView):
    queryset = Model.objects.all() # ここは例
    serializer_class = SampleSerializer

    # 認証に用いる
    permission_classes = [IsAuthenticated]
```
