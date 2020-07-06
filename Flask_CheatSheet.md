# 啟動Flask

set FLASK_APP=flaskr</br>
set FLASK_ENV=development</br>
flask run</br>


# 建立巢狀清單式model
```python
coordinate_field = {}
coordinate_field['x'] = fields.Float
coordinate_field['y'] = fields.Float

boundbox_field = {}
boundbox_field['top_left'] = fields.Float
boundbox_field['top_right'] = fields.Float
boundbox_field['bottom_left'] = fields.Float
boundbox_field['bottom_right'] = fields.Float

face_field = {}
face_field['left_eyes'] = fields.Nested(coordinate_field)
face_field['right_eyes'] = fields.Nested(coordinate_field)
face_field['nose'] = fields.Nested(coordinate_field)
face_field['mouth_left'] = fields.Nested(coordinate_field)
face_field['mouth_right'] = fields.Nested(coordinate_field)
face_field['boundingbox'] = fields.Nested(boundbox_field)

faces_field = {}
faces_field['counts'] = fields.Integer
faces_field['face'] = fields.List(fields.Nested(face_field))
```
