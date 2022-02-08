---
layout: post
title: "Polyspace Code Metrics"
categories: [S/W Engineering]
tags: [SW Metrics, Polyspace]
---

Sonargraph의 Metric들을 살펴보다가 그 외 Metric은 어떤 것들이 있는지 궁금해졌다. Polyspace의 Metric들을 살펴봤는데, Understand와 마찬가지로 Sonargraph의 Metric 보다는 단순하다. 함수 단위로 나오는 Metric이 많다는 것도 단점. 전체를 볼 수 있는 Project Metric이 부족하다. Metric들의 컨셉은 비슷하지만, 계산에 사용하는 용어의 정의라던가 계산 방식은 조금씩 차이가 있다. 어디에 어떻게 쓰는지가 중요하니까 컨셉을 이해하자

* Project Metrics
	* Number of Direct Recursions
		* 직접 재귀(func A -> func A) 덩어리 수. 보통 재귀 함수의 수
	* Number of Header Files
		* 헤더 파일의 수
	* Number of Files
		* 소스 파일의 수
	* Number of Recursions
		* Number of Direct Recursions + 간접 재귀(func A -> func B -> func A) 덩어리 수
* File Metrics
	* Comment Density
		* 코드 라인 수 대비 주석 라인 수
	* Estimated Function Coupling
		* 현재 파일에서, 함수 호출 수 - 함수 정의 수 + 1
			* 함수 정의는 몇 개 안했지만, 호출이 많으면 양수
			* 호출도 안하는데 함수 정의가 많으면 음수
			* 함수가 얼마나 효율적으로 사용되는지 추정
	* Number of Lines
		* 파일의 줄 수. 주석 포함
	* Number of Lines Without Comment
		* 주석을 제외한 파일의 줄 수
* Function Metrics
	* Cyclomatic Complexity
		* 함수 내 의사 결정 분기(if, switch, ...) 수
		* 함수가 얼마나 복잡한지(복잡한 결과를 가지는지) 추정
	* Higher Estimate of Size of Local Variables
		* 함수 내 로컬 변수의 크기의 합(bytes)
			* 리턴 값 사이즈 + 파라미터들 사이즈 + 로컬 변수들 사이즈 + 메모리 alignment padding
		* 함수가 스택을 얼마나 사용하는지 대략 추정
	* Language Scope
		* (operator 발생 수 + operand 발생 수) / (operator 수 + operand 수)
			* 참고로 여기서 operator는 일반적 의미의 operator가 아니라 identifier(변수명, 함수명 등)를 제외한 모든 것으로 정의한다고 함
		* 이 값이 크다면, 중복이 많이 되고 있다는 뜻이다. 4 미만의 값으로 유지하길 권하고 있다.
		```C
		int g(int);
		int f(int i)
		{
		    if (i == 1)
		        return i;
		    else
		        return i * g(i-1);
		}
		```
		* int g(int);는 declaration이니 제외하고, 그 이후 define에 해당하는 부분부터 계산하면
			* operator 발생 수 : 19
				* int ( int ) { if ( == ) return ; else return * ( - ) ; }
			* operand 발생 수 : 9
				* f i i 1 i i g i 1
			* operator 수 : 12
				* int ( ) { if == return else * - ; }
			* operand 수 : 4
				* f i 1 g
			* 따라서 Langauge Scope = (19 + 9) / (12+4) = 1.8
	* Lower Estimate of Size of Local Variables
		* Higher Estimate of Size of Local Variables와 비슷
		* 로컬 변수들 사이즈를 계산할 때, 예를 들어 switch 조건에 따라 갈리는 루틴이 있다고 하면, 각 case에 정의된 변수가 동시에 모두 스택에 쌓여 사용되는 것이 아니기 때문에, 가장 큰 값만 취하고, 나머지는 계산에서 제외하는 것이 더 정확할 수 있다
	* Number of Call Levels
		* if, switch, for 등으로 만들어지는 depth의 깊이
	* Number of Call Occurrences
		* 함수 내에서 함수 호출 수
		* 함수 A를 여러번 호출 했으면 모두 계산 됨
	* Number of Called Functions
		* 함수 내에서 호출된 함수의 수
		* 함수 A를 여러번 호출했으면 한번만 계산됨
	* Number of Calling Functions
		* 해당 함수가 호출된 수
	* Number of Executable Lines
		* 함수 내에서 declaration, 주석, 빈줄, 괄호, pre-processing 문구 등을 제거한 줄 수
	* Number of Function Parameters
		* 함수 파라미터 수
	* Number of Goto Statements
		* goto 문 수
	* Number of Instructions
		* 인스트럭션의 수
		* 마찬가지로 인스트럭션의 의미를 재정의 한다고 함
			* 세미콜론(;)으로 끝나는 statement
			* static 아닌, 초기화된 변수
			* 흐름 제어 statement(if, for, break, goto, return, switch, while, do-while 등)
			* case와 같은 label은 포함되지 않음
		* 50이하 권장
	* Number of Lines Within Body
		* 함수 내 줄 수
	* Number of Local Non-Static Variables
		* 함수 내 non-static 변수 수
	* Number of Local Static Variables
		* 함수 내 static 변수 수
	* Number of Paths
		* 함수 내 코드 수행 경로의 수
		* if, switch, for 등을 만나면 경로가 갈린다. 만날 때마다 곱으로 계산한다
		* if {} else {} 가 있으면 Number of Paths 는 2다
		* if { if {} else {} } else {} 가 있으면 Number of Paths는 1 x 2 + 1 = 3
	* Number of Return Statements
		* return 문의 수
	* 참고
		* https://kr.mathworks.com/help/bugfinder/metrics-reference.html?s_tid=CRUX_lftnav