# 스프링 프레임워크 입문


## Inversion of Control

의존성에 대한 컨트롤이 뒤바뀌었다.

원래는 어떻게 되어있었길래 뒤바뀌었다고 말을 할 수 있는가

어떻게 만든게 뒤바뀐건가?



원래 의존성에 대한 제어권은 자기자신에게 있다.

Ioc를 하지 않았더라면 다음과 같이 new해서 사용을 했는데

(오너리포지토리는 오너컨트롤러의 의존성이다. 오너리포지토리가 있어야 오너 컨트롤러를 쓸 수 있다. 오너컨트롤러는 오너리포지토리를 필요로한다.)

```java
class OwnerController {
	private OwnerRepository repository = new OwenrRepository();
}
```

이러한 의존성을 누가 만드느냐 누가 관리하느냐가 관건이다!

나한테 의존성 제어권이 있었는데 더이상 내가 관리하지 않겠다 => IoC

- 내가 쓸 놈의 하위 타입이면 바꿔끼기 좋지 않겠어?
- 그래야 내 코드 테스트 하기도 편하지



레퍼런스 타입의 변수만 들고 누군가가 생성자로 값을 주겠지 라고 가정을 하고 나머지 코드에서 repo를 사용하면 된다.

다음과 같은 코드의 형태가 의존성 관리가 IoC이다.

나 자신이 아닌 나아닌 누군가로 제어권이 넘어간다!

```java
class OwnerController {
	private OwnerRepository repo;
}

public OwnerController(OwnerRepository repo) {
    this.repo = repo;
}
```

```java
class OwnerControllerTest {
	@Test
	public void create() {
        //오너리포지토리를 만들어서 오너 컨트롤러한테 생성자를 통해 넘겨준다 => 의존성 주입
		OwnerRepository repo = new OwnerRepository();
		OwnerController controller = new OwnerController(repo); //의존성주입
	}
}
```

