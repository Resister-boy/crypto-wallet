## 블록체인 지갑이란?
> 블록체인 지갑은 블록체인과 사용자들의 상호작용을 도와주는 애플리케이션이며, 여러 종류의 블록체인 애플리케이션 중에서도 가장 빈번하게 사용된다. 사용자는 지갑을 통해 블록체인 상 자신의 신원을 의미하는 주소, 트랜젝션, 잔액 등을 확인할 수 있다. 지갑에서 확인할 수 있는 토큰이나 코인은 지갑 서버에 저장되는 것이 아니며, 지갑 서버에는 사용자의 지갑주소를 의미하는 공개키와 개인키만이 저장된다. 

### 공개키
> 전통적인 은행 애플리케이션의 계좌번호의 역할을 하며, 온체인 상에서 사용자의 신원을 의미한다. 일반적으로 개인키에 암호학 알고리즘을 적용하여 개인키를 기반으로 만들어진다. 대표적으로 타원곡선 알고리즘이나, RSA가 있다.

### 개인키
> 랜덤한 숫자나 단어를 해싱하여 만들어진다. 일반적으로 랜덤한 단어를 해싱하여 만들어지는데, 이는 사용자가 디코딩한 개인키를 기억하기 쉽도록 하기 위함이며, 임의의 값을 해싱하는 이유는 일차적으로 오리지널 텍스트를 가리기 위한 보안적인 이유도 있지만, 개인키가 정해진 길이의 문자열의 형태여야 하기 때문이다.

### 트랜젝션 인증 프로세스
> 특정 공개키로 만들어낸 트랜젝션은 해당하는 공개키에 의해 해싱된다. 이 트랜젝션의 해시값은 오직 해당 공개키에 대응하는 개인키로만 디코딩이 가능하며, 다른 개인키로는 트랜젝션을 디코딩할 수 없다. 지갑은 이런 방식으로 트랜젝션을 검증한다.

### 지갑 종류
- Hardware vs Software
- Cold vs Hot
- Self-Custody vs Third Party

### 지갑 주소(공개키) 생성
> 지갑을 생성하는데 사용되는 함수는 단방향 함수로서, 함수가 적용된 값을 알더라도 해당 값의 역을 만들어내는 것이 암호학적으로 불가능한 구조이다. 이때, 암호학적으로 불가능하다는 것은 역을 추적하기 위해 천문학적인 컴퓨팅 자원과 시간이 소모되어 경제적이지 않다는 것을 의미한다. 일반적으로 개인키에서 공개키를 만들 때는 Elliptic Curve Multiplicaton을 사용하고, 공갴에서 주소를 만들 때는 Hashing Function(20 ~ 32byte의 문자열 반환)을 사용한다. 


### 니모닉 코드
> 지갑을 쉽게 복구하기 위한 단어를 의미하며, 니모닉 코드는 프라이빗키를 생성하는데 필요한 시드를 구성하는 구문이라고 할 수 있다. 즉, 니모닉 코드가 프라이빗키를 의미하는 것은 아니다. 다만, 니모닉 코드의 유출은 프라이빗키를 유출하는 것과 같다고 할 수 있다.  

### 니모닉 코드의 생성
> 니모닉 코드는 엔트로피라고 불리는 랜덤한 값에서 생성된다. 엔트로피는 난수 생성 프로그램을 통해 만들어지며, 이렇게 만들어진 난수를 SHA256으로 해싱하여 각 세그먼트를 나누고, 이를 특정한 단어에 매핑한 것이 바로 니모닉 코드라고 할 수 있다. 니모닉 코드에 sort함수를 적용한 것이 시드구문이 된다.

### HD Wallet(계층 결정적 지갑)
> 계층 결정적 지갑은 하나의 개인키로 만들어진 여러 공개키들을 의미한다. 이때 개인키와 공개키 사이에는 마스터키라는 중간 계층이 존재한다. 이때 마스터키는 KDF라는 키 생성 알고리즘을 통해 만들어진다.