# Class

* 인터페이스와 생성자를 통한 옵셔널 프로퍼티 설정

```typescript
// 생성자를 통해 받을 옵셔널 데이터들
interface Props {
    a?: number;
    b?: number;
    aa?: 'aa' | 'aaa';
    bb?: 'bb' | 'bbb';
}

class A {
    a?: number;
    aa?: 'aa'|'aaa';
}

class B extends A {
    b?: number;
    bb?: 'bb'|'bbb';
    boolTest: boolean;

    // Props 에 선언된 프로퍼티만 설정 가능
    constructor(props?: Props) {
        super(); // super에도 props 넘겨줄수있다
        this.boolTest = false;
        Object.assign(this, props);
    }
}

// ?를 이용한 옵셔널 값들은 안넘겨줘도 된다.
let test = new B({
    a: 1,
    aa: 'aa'
});
```
