### 생성자 vs static 메소드

#### 비교
| 생성자 | static 메소드 |
| --- | --- |
| 별도의 이름을 가질 수 없음 | 별도의 이름을 가질 수 있음 |
| 똑같은 타입 2개를 받는 별도의 생성자 생성 불가 new Line(int x, int y) vs new Line(int y, int x) | 똑같은 타입 2개를 받더라도 생성 가능 LineBuilder.setX(x).setY(y).build() |
| 반드시 새 객체를 생성해야 함 | 반드시 새 객체를 생성할 필요 없음(builder 내부의 상수 객체를 리턴할 수 있음) |
|  | 리턴 타입의 하위 객체를 리턴할 수 있다. |
|  | javadoc으로 관리되지 않는다. |

#### 생성자
CustomClass instance1 = new CustomClass();

CustomClass1 instance2 = new CustomClass((int) value1, (int) value2);

#### static 메소드
CustomClass instance1 = CustomClass
							.newInstance();

CustomClass {
	public static CustomClass newInstance(){
		return new CustomClass();
	}
}

CustomClass1 instance2 = CustomClass1
							.newInstanceType1((int) value1, (int) value2);
CustomClass1 instance3 = CustomClass1
							.newInstanceType2((int) value2, (int) value1);

CustomClass1 {
	public static CustomClass1 newInstanceType1(int value1, int value2){
		CustomClass1 instance = new CustomClass1();

		instance.setValue1(value1);
		instance.setValue2(value2);

		return instance;
	}

	public static CustomClass1 newInstanceType2(int value2, int value1){
		CustomClass1 instance = new CustomClass1();

        instance.setValue1(value1);
        instance.setValue2(value2);

        return instance;
	}
}

CustomClass2 instance4 = CustomClass2
							.getInstance();

CustomClass2 {
	private static final CustomClass2 DEFAULT_INSTANCE = new CustomClass2();

	public static CustomClass2 getInstance(){
		return DEFAULT_INSTANCE;
	}
}

//절대 좋은 코드는 아님 샘플을 위한 코드
ClassA instance5 = ClassA
				.newInstance(true);
ClassA instance6 = ClassA
				.newInstance(false);

private static class ClassA {
		public static ClassA newInstance(boolean tnf) {
			if (tnf) {
				return new ClassB();
			} else {
				return new ClassC();
			}
		}
	}

	private static class ClassB extends ClassA {
	}

	private static class ClassC extends ClassA {
	}