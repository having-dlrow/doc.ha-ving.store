# Validation

## <mark style="color:blue;">@valid</mark>

### 빈값 체크

<table><thead><tr><th width="159"></th><th></th></tr></thead><tbody><tr><td>@NotNull</td><td>반드시 값이 있어야 한다.</td></tr><tr><td>@NotEmpty</td><td>반드시 값이 존재하고 길이 혹은 크기가 0보다 커야한다.</td></tr><tr><td>@NotBlank</td><td>반드시 값이 존재하고 공백 문자를 제외한 길이가 0보다 커야 한다.</td></tr></tbody></table>

|           | null  | ""    | " "   |
| --------- | ----- | ----- | ----- |
| @NotNull  | false | true  | true  |
| @NotEmpty | false | false | true  |
| @NotBlank | false | false | false |

## <mark style="color:blue;">jakarta.validation</mark> vs org.springframework.validation

## <mark style="color:blue;">jakarta.validation</mark>

1. 자바 표준 유효성 검사 스펙(Jakarta Bean Validation)을 따른다.
2. 데이터 모델의 유효성 검사에 사용한다.
3. **`@Valid` 을 사용한다.**

## org.springframework.validation

1. org.springframework.validation.Validator 인터페이스와 \
   org.springframework.validation.Errors 인터페이스를 사용하여 커스텀 유효성 검사
2. BindResult , 데이터 모델을 검증한다.
