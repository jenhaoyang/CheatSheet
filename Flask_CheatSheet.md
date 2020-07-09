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

# namespace
```python
from flask import Flask
from flask_restplus import Api, Resource, fields, Model
from werkzeug.contrib.profiler import ProfilerMiddleware

app = Flask(__name__)

api = Api(version='1.0', title='Test')

ns = api.namespace('test')

test_element = api.model('Element', {
    'a': fields.Integer(),
    'b': fields.String(),
})

test_list = api.model('TestList', {
    'data': fields.List(fields.Nested(test_element))
})


@ns.route('/')
class TestCollection(Resource):
    @api.marshal_list_with(test_list)
    def get(self):
        return {
            'data': [
                {'a': x, 'b': x}
                for x in range(0, 1000)
            ]
        }


if __name__ == '__main__':
    app.config['PROFILE'] = True
    app.wsgi_app = ProfilerMiddleware(app.wsgi_app, restrictions=(10, ))

    api.init_app(app)
    api.add_namespace(ns)
    app.run(host='0.0.0.0', debug=True)
```

# 打包成exe
https://elc.github.io/posts/executable-flask-pyinstaller/

https://github.com/jenhaoyang/flask-pyinstaller

pyinstaller --onefile --add-data "templates;templates" --add-data "static;static" --add-data "core/mtcnn_tool/model;core/mtcnn_tool/model" app.py
pyinstaller --onedir --add-data "templates;templates" --add-data "static;static" --add-data "core/mtcnn_tool/model;core/mtcnn_tool/model" app.py
