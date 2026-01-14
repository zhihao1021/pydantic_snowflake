# Pydantic Snowflake ID

A Pydantic custom type for validating and serializing Snowflake IDs.

## Features
- Custom Pydantic type `SnowflakeId` for Snowflake ID validation.
- `SnowflakeGenerator` for generating unique Snowflake IDs.
- Supports custom epochs, worker IDs, and process IDs.
- Supports serialization and deserialization of pydantic models with Snowflake IDs.

## Installation
You can install the package via pip:

```bash
pip install -U pydantic-snowflakes
```

## Usage
```python
from pydantic import BaseModel
from pydantic_snowflake import SnowflakeId, SnowflakeGenerator

from datetime import datetime

custom_epoch = datetime(2020, 1, 1)

class User(BaseModel):
    id: SnowflakeId
    name: str

# Generating a Snowflake ID
generator = SnowflakeGenerator(
    epoch=custom_epoch,
    worker_id=0,
    process_id=0
)

new_id = generator.next()
user = User(id=new_id, name="Alice")
print(user)

# Generating multiple Snowflake IDs
for _id in [generator.next() for _ in range(5)]:
    user = User(id=_id, name="Bob")
    print(user)
```

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details
