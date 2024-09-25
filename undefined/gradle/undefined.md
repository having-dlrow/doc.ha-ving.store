# 의존성 목록



### **spring-boot-starter-validation ( hibernate-validator )**

{% embed url="https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-validation/3.3.4" %}

#### Custom Validator 만들기

```
@Constraint(validatedBy = {NicknameValidator.class})
@Target({METHOD,FIELD, ANNOTATION_TYPE, CONTRUCTOR, PARAMETER, TYPE_USER})
@Retention(RUNTIME)
public @interface NickName {
```

Bean Validation 구조화

```
public abstract class SelfValidation<T> {
    private Validator validator;

    public SelfValidation() {
        ValidatorFactory factory = Validation.buildDefaultValidatorFactory();
        validator = factory.getValidator();
    }

    protected void validateSelf() {
        Set<ConstraintViolation<T>> violations = validator.validate((T) this);
        if (!violations.isEmpty()) {
            throw new ConstraintViolationException(violations);
        }
    }
}
```
