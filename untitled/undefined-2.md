# 제네릭 타입의 형변환

## 제네릭 타입과 원시 자료형간의 형변환은 바람직하지 않음

```
GiftBox giftBox1 = new GiftBox();

		GiftBox<Person> giftBox2 = new GiftBox<Person>();

		giftBox1 = giftBox2;
		giftBox2 = giftBox1;// Type safety: The expression of type GiftBox needs unchecked conversion to
							// conform to GiftBox<Person>
```

### 와일드 카드가 사용된 제네릭 타입으로는 형변환 가능

```bash
		GiftBox<? extends Number> giftBox3 = new GiftBox<Integer>();
	//	GiftBox<Double> giftBox4 = giftBox3;
	// Type mismatch: cannot convert from GiftBox<capture#1-of ? extends Number>
											// to GiftBox<Double>
		GiftBox<Double> giftBox4 =(GiftBox<Double>) giftBox3;
```



