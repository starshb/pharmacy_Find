# 스프링 빈(bean)이란? <br>
- 스프링(Spring) 컨테이너가 관리하는 자바 객체를 빈(Bean)이라 한다.

<hr>
<br>
<br>

# 1. 스프링의 특징에는 제어의 역전(IoC)이 있다. <br>
제어의 역전이란, 간단히 말해서 객체의 생성 및 제어권을 사용자가 아닌 스프링에게 맡기는 것이다. 지금까지는 사용자가 new연산을 통해 객체를 생성하고 메소드를 호출했다. IoC가 적용된 경우에는 이러한 객체의 생성과 사용자의 제어권을 스프링에게 넘긴다. 사용자는 직접 new를 이용해 생성한 객체를 사용하지 않고, 스프링에 의하여 관리당하는 자바 객체를 사용한다. 이 객체를 '빈(bean)'이라 한다.

<hr>
<br>
<br>

# 2. 스프링 빈(bean)을 스프링 컨테이너에 등록하는 방법 <br>
# 2.1 컴포넌트 스캔과 자동 의존관계 설정
<br>
- @Component 애노테이션이 있으면 스프링 빈으로 자동 등록된다. 또한, @Component를 포함하는 @Controller, @Service, @Repository 애노테이션도 스프링 빈으로 자동 등록된다.

<br>
<br>
<img width="30%" src="https://github.com/starshb/pharmacy_Find/assets/138543543/b932fbc1-a8d8-4fb2-b4a9-7d027ccabf7c"/>
<br>
회원 컨트롤러를 등록하고, 회원 컨트롤러가 회원서비스와 회원 리포지토리를 사용할 수 있게 의존관계를 설정해보자.

예제는 회원 관리 예제 코드를 사용할 것이다.
<br>
<br>

package hello.hellospring.controller;

import hello.hellospring.service.MemberService;<br>
import org.springframework.beans.factory.annotation.Autowired;<br>
import org.springframework.stereotype.Controller;

@Controller
public class MemberController {

    private final MemberService memberService;

	@Autowired
    public MemberController(MemberService memberService) {
        this.memberService = memberService;
    }
}

<br>
<br>
- @Autowired
생성자에 @Autowired가 있으면 스프링이 연관된 객체를 스프링 컨테이너에 찾아서 넣어준다. 이렇게 객체 의존관계를 외부에서 넣어주는 것을 '의존성 주입(DI)'라 한다. 위 관계 그림에서 -> 의존관계를 표현한 화살표 역할을 해준다. (생성자가 1개만 있으면 생략 가능)
회원 관리 예제 때는 개발자가 테스트에서 직접 주입했고, 여기서는 @Autowired에 의해 스프링이 주입해준다.
이 상태로 서버를 작동시키면 오류가 발생함.
<br>
<br>
<img width="30%" src="https://github.com/starshb/MarryU/assets/138543543/c766d71f-d3f8-40bc-9a6c-f528f5f44753"/>
<br>
바로 memberService가 스프링 컨테이너에 스프링 빈으로 등록되어 있지 않기 때문이다.
memberService도 스프링 빈으로 등록해주어야 한다.
<br>
<hr>

@Service
public class MemberService {

	private final MemberRepository memberRepository;

	@Autowired
	public MemberService(MemberRepository memberRepository) {
		this.memberRepository = memberRepository;
	}
}

<br>
<hr>
memberRepository도 스프링 빈으로 등록해야 한다.
<br>
<hr>
@Repository
public class MemoryMemberRepository implements MemberRepository {}
<br>
<hr>
<img width="30%" src="https://github.com/starshb/MarryU/assets/138543543/c4bb6d9e-9248-43ff-a1f1-e6035ea73c13"/>
<br>
<hr>
memberService와 memberRepository가 스프링 컨테이너에 스프링 빈으로 등록되었다.

참고로, 스프링은 스프링 컨테이너에 스프링 빈을 등록할 때, 기본으로 싱글톤으로 등록한다.(유일하게 하나만 등록해서 공유한다.) 따라서 같은 스프링 빈이면 모두 같은 인스턴스다. 설정으로 싱글톤이 아니게 설정할 수 있지만, 특별한 경우를 제외하면 대부분 싱글톤을 사용한다.
<br>
<hr>

# 2.2 자바 코드로 직접 스프링 빈 등록하기(Configuration)
@Configuration과 @Bean 애노테이션을 이용해 스프링 빈을 등록한다. <br>
@Configuration을 이용하면 스프링 프로젝터에서 Configuration 역할을 하는 Class를 지정할 수 있다.
<br>
src/main/java 하위폴더에 SpringConfig 파일을 생성하고 다음과 같이 코드를 작성했다.
<hr>
<br>
package hello.hellospring.service;

import hello.hellospring.repository.MemberRepository;
import hello.hellospring.repository.MemoryMemberRepository;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class SpringConfig {

    @Bean
    public  MemberService memberService() {
        return new MemberService(memberRepository());
    }

    @Bean
    public MemberRepository memberRepository() {
        return new MemoryMemberRepository();
    }
}
