**제로초님의 NestJS 강의를 듣던중..실무에서 사용했던 방법과 다르게 사용하는 부분이 있어서 기록하기 위해 작성중..**:open_mouth:<br><br>
기존 실무에서 Entity는 디비 테이블의 컬럼들을 작성했었고 Dto에는 검증을 하기 위한 데코레이터를 사용하여 작성했었다.<br>
결국, Entity와 Dto는 중복되는 컬럼들이 존재하였지만 2가지로 분리하여 사용하다보니 크게 번거롭진 않았다.<br>
* **기존에 사용하던 Entity 방식**
```
@Entity('users')
export class Users {
  @PrimaryGeneratedColumn()
  @Type(() => Number)
  id!: number;

  @Column({ name: 'name' })
  name!: string;

  @Column({ name: 'level', type: 'enum', enum: Level })
  level!: Country;

  @Column({ name: 'password' })
  password!: string;
}
```

* **기존에 사용하던 Dto 방식**
```
export class CompanyCreateDto {
  @MinLength(1)
  @IsString()
  name!: string;

  @IsEnum(Level)
  level!: Level;

  @MinLength(5)
  @IsString()
  password!: string;
}
```
<br>

헌데, 제로초님의 강의에서는 Dto 클래스에 PickType을 사용하여 Entity를 상속했다. <br>
PickType은 상속받는 Entity에서 중복되는 컬럼들을 넣으면 Entity에 작성되어 있는 컬럼을 Dto에 동일하게 작성하지 않아도 되었다.<br>
또한, Entity에 타입 검증을 하는 데코레이터도 넣었다.<br>
[:point_right: **PickType 공식문서 바로가기**](https://docs.nestjs.com/openapi/mapped-types)
* **새롭게 알게된 Entity 방식**
```
@Index('email', ['email'], { unique: true })
@Entity({ schema: 'sleact', name: 'users' })
export class Users {
  @ApiProperty({
    example: 1,
    description: '사용자 아이디',
  })
  @PrimaryGeneratedColumn({ type: 'int', name: 'id' })
  id: number;

  @IsEmail()
  @ApiProperty({
    example: 'zerohch@gmail.com',
    description: '이메일',
  })
  @Column('varchar', { name: 'email', unique: true, length: 30 })
  email: string;

  @IsString()
  @IsNotEmpty()
  @ApiProperty({
    example: ' 제로초',
    description: '닉네임',
  })
  @Column('varchar', { name: 'nickname', length: 30 })
  nickname: string;

  @Column('varchar', { name: 'password', length: 100, select: false })
  password: string;

  @CreateDateColumn()
  createdAt: Date;

  @UpdateDateColumn()
  updatedAt: Date;

  @DeleteDateColumn()
  deletedAt: Date | null;
}
```

* **새롭게 알게된 Dto 방식**
```
export class JoinRequestDto extends PickType(Users, [
  'email',
  'nickname',
  'password',
] as const) {}
```
<br>

여기서 또 궁금증들이 생겼다. 확실히 중복되는 코드는 없어지기 때문에 코드는 간략해지지만 선택 옵션과 타입 검증을 위한 데코레이터들을 Entity에 작성하는게 맞는지 생각하게 되었고 궁금해서 제로초님께 질문을 남겼었고 아래 답변을 받았다.<br>
> 엔티티는 db의 테이블을 클래스로 매핑한 것이고(저는 relation까지는 같이 넣어두는 편이긴 합니다) dto는 계층간 데이터 전달을 위해 좀 더 범용적으로 쓰이는 객체가 맞습니다. dto쪽에 비즈니스적 검증로직을 몰아두는 게 좋긴 합니다. entity에는 실제 디비에 저장하기 위한 필수적인 조건 검증로직만 붙여놓고요.

<br>
내가 알고 있던 지식보다 조금 더 구체적으로 파악할 수 있었고 강의에서 사용했던 방식은 NestJS에서 제공해주기 때문에 알려주기 위함이였던 것 같다. 뭐든 많이 알고 있으면 상황에 따라 사용할 수 있는 지식의 범위가 넓어지는 것이라고 생각한다.
