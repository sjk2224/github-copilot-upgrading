# upgraded 폴더 구조 설명

`upgraded` 폴더는 레거시(`legacy`) 폴더의 전체 파일 및 디렉터리 구조를 그대로 복사한 디렉터리입니다. 각 하위 폴더 및 파일의 역할은 다음과 같습니다.

## 최상위 파일 및 폴더
- `MANIFEST.in`: 패키징 시 포함할 파일 목록을 지정하는 파일
- `README.rst`: 프로젝트 설명 파일 (reStructuredText 형식)
- `distribute-0.6.10.tar.gz`, `distribute_setup.py`: 레거시 Python 패키징 도구 관련 파일
- `setup.py`: 프로젝트 설치 및 배포를 위한 스크립트
- `docs/`: 프로젝트 문서 관련 폴더
- `guachi/`: 주요 소스 코드 및 테스트 폴더
- `guachi.egg-info/`: 패키징 메타데이터 폴더

## docs/
- `Makefile`: 문서 빌드 자동화 파일
- `build/`: 빌드된 문서(HTML, doctree 등) 저장 폴더
  - `doctrees/`: Sphinx 문서 빌드 중간 산출물
  - `html/`: HTML 문서 결과물
    - `_sources/`: rst 원본 텍스트
    - `_static/`: 정적 파일(css, js, 이미지 등)
- `source/`: 문서 원본(rst, conf.py 등)
  - `_static/`: 사용자 정의 CSS 등 정적 파일

## guachi/
- `__init__.py`, `config.py`, `database.py`: 주요 Python 모듈
- `tests/`: 유닛 테스트 코드
  - `test_configmapper.py`, `test_configurations.py`, `test_database.py`, `test_integration.py`: 각 기능별 테스트 파일

## guachi.egg-info/
- 패키징 및 배포를 위한 메타데이터 파일들

---

이 폴더는 레거시 코드를 최신 Python 환경에 맞게 업그레이드하거나 실험할 때 안전하게 사용할 수 있도록 별도로 복사된 공간입니다.