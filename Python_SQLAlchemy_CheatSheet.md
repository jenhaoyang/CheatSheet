## 初始化db
init
upgrade
migrate

## 刪除Table的每個row
```python
    def delete(self):
        """
        Delete all person by ID.
        """
        with api.commit_or_abort(
                db.session,
                default_error_message="Failed to delete all person."
            ):
            #people = Person.query.all()
            db.session.query(Person).delete()
        return None
  ```
