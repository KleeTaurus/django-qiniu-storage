django-qiniu-storage
=====================

This simple app demostrate how to make Django play well with Qiniu cloud storage.

## Requirements ##

1. django(1.6.6)
2. qiniu(6.1.8)
3. django-qiniu-storage(0.1.0)
4. requests==2.4.0

## Installation guide ##

* Create a new virtual environment

    ```
    virtualenv env
    source env/bin/activiate
    ```

* Install third-party libraries

    ```
    pip install -r cloudstorage/requirements.txt
    ```

## Notes ##

You should modify the source code in backends.py yourself, the file_stat should not raise an IOError when the file does not exist, since django will call it automaticlly before saving the file.

```
def _file_stat(self, name):
        name = self._clean_name(name)
        ret, err = qiniu.rs.Client().stat(self.bucket_name, name)
        """
        if err:
            raise IOError(
                "Failed to get stats of file '%s'. "
                "Error message: %s" % (name, err))
        """
        return ret
```
