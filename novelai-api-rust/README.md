# Setup

`novelai-api-rust`는 `.env`파일로부터 클라이언트 정보를 불러옵니다. 따라서 해당 파일을 수정해야 API를 사용할 수 있습니다. 초기의 `.env` 파일 내부는 다음과 같이 작성되어 있습니다.

```bash
USERNAME=NOVELAI_UESRNAME
PASSWORD=NOVELAI_PASSWORD
```

`NOVELAI_USERNAME` 필드와 `NOVELAI_PASSWORD` 필드를 자신의 NovelAI 계정명과 비밀번호로 바꿔야 합니다.

> [!WARNING]
>  저장된 계정명과 비밀번호는 타인에게 노출될 수 있으므로 안전한 환경에서만 사용해야 합니다.

그 다음, 자신의 프로그램 안에서 저장된 계정 이름과 비밀번호를 다음과 같이 불러와야 합니다.

```rust
let username = dotenv::var("USERNAME").unwrap();
let password = dotenv::var("PASSWORD").unwrap();
```

`username`과 `password`는 이후 클라이언트 인터페이스를 설정하는 데 사용됩니다.

# `struct NAIClient`


NovelAI API와 통신하는 클라이언트 인터페이스.
## usage

해당 구조체는 다음과 같이 `import`해서 사용할 수 있습니다.

```rust
use novelai::client::NAIClient

#[tokio::main]
async fn main() {
	dotenv::dotenv().ok();

	let username = dotenv::var("USERNAME").unwrap();
	let password = dotenv::var("PASSWORD").unwrap();
	
	let client = NAIClient::new(&username, &password);
}
```

이미지를 생성하기 위해서는 `generate_image()`메서드를 사용해야 합니다. 해당 메서드를 사용하기 위해, 이미지 설정 구조체인 `ImagePreset`과 `Parameters`를 가져와야 합니다. 해당 구조체들은 모두 빌더를 통해 속성들을 제어할 수 있습니다.

```rust
use novelai::preset::{ImagePresetBuilder, ParametersBuilder};

let params = ParametersBuilder::new().build();

let perset = ImagePresetBuilder::new()
		.prompt(String::from("1girl"))
		.parameters(params)
		.build();

let _ = client.generate_image(preset).await;
```

# `struct ImagePreset`

이미지를 생성하는 데 필요한 설정들을 모아놓은 구조체. 

1. `prompt`:  
2. `model`:
3. `parameters`: 