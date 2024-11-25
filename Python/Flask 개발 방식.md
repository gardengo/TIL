# Flask 백엔드 개발 가이드

## 1. Flask 라우팅 방식 비교

### @app.route 방식

- 간단한 URL 매핑
- 빠른 구현 가능
- 작은 프로젝트에 적합

```python
@app.route('/users', methods=['GET'])
def get_users():
    return 'Users list'
```

### RESTful API 방식

- Resource 기반 클래스 구조
- 체계적인 API 관리
- 대규모 프로젝트에 적합

```python
from flask_restful import Api, Resource

class UserResource(Resource):
    def get(self):
        return 'Users list'
```

## 2. 레이어드 아키텍처 구조

### 프로젝트 구조

```
/api
  /view        # API 엔드포인트
  /service     # 비즈니스 로직
  /model       # 데이터베이스 모델
  app.py       # 메인 애플리케이션
```

### ORM 연동 예시

```python
class UserModel(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(80))
    email = db.Column(db.String(120))

class UserResource(Resource):
    def get(self, user_id):
        user = UserModel.query.get(user_id)
        return {'name': user.name, 'email': user.email}
```

## 3. Python 백엔드 개발의 장점

### 개발 효율성

- 간단하고 직관적인 문법
- 빠른 개발 속도
- 쉬운 유지보수

### 풍부한 생태계

- 다양한 라이브러리 지원
- 강력한 웹 프레임워크
- AI/ML 통합 용이

### 확장성

- 대규모 서비스 지원
- 크로스 플랫폼 호환
- 다양한 기술 스택과 통합 가능

## 4. 사용 사례

- Instagram
- Netflix
- Google
- Airbnb
- Uber

이러한 구조와 특징으로 인해 Python/Flask는 현대적인 백엔드 개발에 매우 적합한 선택지가 됩니다.