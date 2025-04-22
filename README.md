# Salamon – AI‑gestützter Yu‑Gi‑Oh!™‑Deck‑Generator

## Paketinstallation

### Benötigte Python-Pakete installieren

```bash
# Installiere alle erforderlichen Abhängigkeiten
pip install fastapi uvicorn sqlalchemy pydantic requests numpy
```


## SQLite-Einrichtung

### SQLite als Dialekt konfigurieren

Die Anwendung ist bereits für SQLite konfiguriert. Der Dialekt wird in der Datei `db/db.py` definiert:

```python
# db/db.py
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker
from contextlib import contextmanager

# SQLite-Dialekt ist hier konfiguriert
DATABASE_URL = "sqlite:///data.sqlite"  
engine = create_engine(DATABASE_URL, connect_args={"check_same_thread": False})

SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)

@contextmanager
def get_session():
    session = SessionLocal()
    try:
        yield session
    finally:
        session.close()
```


