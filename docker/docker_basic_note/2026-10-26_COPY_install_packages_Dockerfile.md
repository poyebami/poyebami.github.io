<h1>Copy Command to Install packages</h1>
If the project has a requirements.txt and also needs 
```console
 COPY requirements.txt .
 RUN pip install --no-cache-dir -r requirements.txt
 ```

