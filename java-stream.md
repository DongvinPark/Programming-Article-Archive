# Java Stream API Exampler Archive

<br><br/>
- 자바 8 버전에서 최초로 도입된 스트림의 기본적인 사용 예시들을 하나의 클래스 안에 모아 놓은 프로그램 코드 입니다.

<br><br/>
- 자세한 설명은 코드 내 주석에 기재하였습니다.

```java
package test;

import java.util.*;

import java.util.function.Predicate;
import java.util.stream.Collectors;
import java.util.stream.IntStream;
import java.util.stream.Stream;

import test.Phase.Transition;


public class MyTest {
    public static void main(String[] args) {
    	//오늘 자바 스트림의 사용법들하고 끝장을 보겠다.
      
      /* 프로그램 실행 결과는 아래와 같다.
***** 인트 타입 배열에서 스트림 활용하기 시작!!
최댓값 : 75
최솟값 : -57
평균값 : 8.75
10이상 70이상 숫자들 전부 찾기 : [14, 24, 56, 65]
12와의 차이의 절댓값이 작은 순서대로 나열 : [14, 9, 8, 6, 4, 3, 2, 1, 0, 24, -3, -4, -5, -6, -8, -9, 56, 65, 75, -57]
[-57, -9, -8, -6, -5, -4, -3, 0, 1, 2, 3, 4, 6, 8, 9, 14, 24, 56, 65, 75]
내림자순 정렬 : [75, 65, 56, 24, 14, 9, 8, 6, 4, 3, 2, 1, 0, -3, -4, -5, -6, -8, -9, -57]
소수 찾기 : [3, 2]
소수 아닌 수들 찾기 : [56, -5, -57, 1, 75, 4, -8, -3, 6, 0, -9, 24, -6, 8, -4, 9, 65, 14]
리스트로 바꾸기 : [56, 3, -5, -57, 1, 75, 4, -8, 2, -3, 6, 0, -9, 24, -6, 8, -4, 9, 65, 14]
리스트를 다시 배열로 바꾸기 : [56, 3, -5, -57, 1, 75, 4, -8, 2, -3, 6, 0, -9, 24, -6, 8, -4, 9, 65, 14]
홀수만 찾아서 배열로 바꾸기 : [3, 1, 75, 9, 65]
짝수만 찾아서 리스트로 바꾸기 : [56, 4, -8, 2, 6, 0, 24, -6, 8, -4, 14]
75
NULL
[56, 3, -5, -57, 1, 75, 4, -8, 2, -3, 6, 0, -9, 24, -6, 8, -4, 9, 65, 14]





***** 2차 배열과 2차 리스트 간의 상호 변환 테스트 시작!!
[0, 1]
[2, 3]
[4, 5, 99]
[6, 7]
[8, 9]
[0, 1]
[2, 3]
[4, 5, 99]
[6, 7]
[8, 9]





***** Integer 타입 리스트에서 스트림 사용법 테스트 시작!!!
최댓값 : 75
평균값 : 8.75
10이상 70이하인 값들 모아서 오름차순 정렬 : [14, 24, 56, 65]
12와의 차이의 절댓값이 작은 순서대로 나열 : [14, 9, 8, 6, 4, 3, 2, 1, 0, 24, -3, -4, -5, -6, -8, -9, 56, 65, 75, -57]
오름차순 정렬 : [-57, -9, -8, -6, -5, -4, -3, 0, 1, 2, 3, 4, 6, 8, 9, 14, 24, 56, 65, 75]
내림차순 정렬 : [75, 65, 56, 24, 14, 9, 8, 6, 4, 3, 2, 1, 0, -3, -4, -5, -6, -8, -9, -57]
소수 모음 : [3, 2]
소수 아닌 수 모음 : [56, -5, -57, 1, 75, 4, -8, -3, 6, 0, -9, 24, -6, 8, -4, 9, 65, 14]
리스트를 배열로. : [56, 3, -5, -57, 1, 75, 4, -8, 2, -3, 6, 0, -9, 24, -6, 8, -4, 9, 65, 14]
홀수만 모으기. : [3, 1, 75, 9, 65]
짝수만 모으기. : [3, 1, 75, 9, 65]
75
NULL
[56, 3, -5, -57, 1, 75, 4, -8, 2, -3, 6, 0, -9, 24, -6, 8, -4, 9, 65, 14]





***** 스트링 배열에 대한 스트림 기초 사용법 테스트 시작!!
전부 대문자로 바꾸기. : [RED, ORANGE, YELLOW, GREEN, BLUE, INDIGO, VIOLET]
m보다 나중에 등장하는 단어들만 모아서 사전순 정렬 : [orange, Red, Violet, Yellow]
m보다 나중에 등장하는 단어들만 모아서 대소문자 무관하게 사전의 역순으로 정렬 : [Yellow, Violet, Red, orange]





***** 스트림을 활요하여 중첩된 맵을 초기화하는 방법 테스트 시작!!
MELT

바깥 맵의 키 들을 전부 출력해보자.
SOLID
LIQUID
GAS
바깥 맵의 키들을 바탕으로, 안쪽 맵들의 키들을 전부 찾아보자.
[LIQUID, GAS]
[SOLID, GAS]
[SOLID, LIQUID]
바깥 맵의 키들을 바탕으로, 안쪽 맵들의 값들을 전부 찾아보자.
[MELT, SUBLIME]
[FREEZE, BOIL]
[DEPOSIT, CONDENSE]
      
      */
    	
    	
    	System.out.println("***** 인트 타입 배열에서 스트림 활용하기 시작!!");
    	int[] intNums = {56,3,-5,-57,1,75,4,-8,2,-3,6,0,-9,24,-6,8,-4,9,65,14};
    	
    	//최댓값을 찾으시오. 이때 getAsInt() 또는 getAsDouble()이 없으면 Optional 타입으로 결과물을 받게 됨.
    	System.out.println("최댓값 : " + 
    			Arrays.stream(intNums).max().getAsInt()
    			);
    	
    	//최솟값을 찾으시오
    	System.out.println("최솟값 : " +
    			Arrays.stream(intNums).min().getAsInt()
    			);
    	
    	//평균값을 찾으시오
    	System.out.println("평균값 : " +
    			Arrays.stream(intNums).average().getAsDouble()
    			);
    	
    	//닫힌 구간 10~70 이내의 숫자들만 골라낸 후 오름차순으로 정렬하여 반환하시오.
    	Predicate<Integer> tenToSeventy = e -> ( 10 <= e && e <= 70);
    	System.out.println("10이상 70이상 숫자들 전부 찾기 : " +
			Arrays.stream(intNums).boxed().sorted().filter(tenToSeventy).collect(Collectors.toList())
    			);
    			
    	
    	//위의 값들을 12와의 차이의 절댓값이 작은 순서대로 나열하시오.
    	//이때, 베이스 타입인 인트 타입으로는 sorted()메서드에 람다식으로 명시한 정렬
    	//규칙을 바로 적용할 수는 없으므로 boxed()를 중간에 끼워줘야 함.
    	System.out.println("12와의 차이의 절댓값이 작은 순서대로 나열 : " +
    			Arrays.stream(intNums).boxed().sorted(
    					(x,y) -> ( Math.abs(x-12) - Math.abs(y-12) )
    					).collect(Collectors.toList())
    			);
    	
    	//오름차순으로 정렬하시오
    	System.out.println(
 			Arrays.stream(intNums).sorted().boxed().collect(Collectors.toList())
    			);
    	
    	//내림차순으로 정렬하시오
    	//이때도 역시 내림차순 정렬기능을 제공하는 Collections.reverseOrder()가
    	//베이스 타입인 인트 타입을 인자로 받아들이지를 못해서 intNums 의 요소들을
    	//Integer라는 박스 타입(==wrapper type)으로 바꿔주는 boxed()메서드를
    	//써줘야 함.
    	System.out.println("내림자순 정렬 : " +
    					Arrays.stream(intNums).boxed().sorted(
    	    					Collections.reverseOrder()
    	    					).collect(Collectors.toList())
    			);
    	
    	//소수인 수를 찾으시오
    	System.out.println("소수 찾기 : " +
    			Arrays.stream(intNums).filter( x -> isPrime(x)).boxed().collect(Collectors.toList())
    			);
    	
    	//소수가 아닌 수를 찾으시오
    	System.out.println("소수 아닌 수들 찾기 : " +
    			Arrays.stream(intNums).filter( x -> isPrime(x)==false).boxed().collect(Collectors.toList())
    			);
    	
    	//리스트로 바꾸시오
    	List<Integer> intToIntegerList = Arrays.stream(intNums).boxed().collect(Collectors.toList());
    	System.out.println(
    			"리스트로 바꾸기 : " +
    			intToIntegerList
    			);
    	
    	//리스트를 다시 배열로 바꾸시오
    	int[] boxedIntToIntArray = intToIntegerList.stream().mapToInt(x -> x).toArray();
    	System.out.println(
    			"리스트를 다시 배열로 바꾸기 : " +
    			Arrays.toString( boxedIntToIntArray )
    			);
    	
    	//홀수를 찾아서 배열형태로 반환하시오.
    	int[] oddNumsArr = Arrays.stream(intNums).filter(
    			x -> (x%2 == 1)
    			).toArray();
    	System.out.println(
    			"홀수만 찾아서 배열로 바꾸기 : " +
    			Arrays.stream(oddNumsArr).boxed().collect(Collectors.toList())
    			);
    	
    	//짝수를 찾아서 리스트 형태로 반환하시오.
    	List<Integer> evenNumList = Arrays.stream(intNums).filter(
    			x -> (x%2 == 0)
    			).boxed().collect(Collectors.toList());
    	System.out.println("짝수만 찾아서 리스트로 바꾸기 : " +evenNumList);
    	
    	
    	//홀수 중 최댓값을 찾으시오. 찾지 못한 경우에 대해서도 처리하시오.
    	//홀수가 하나도 없을 수도 있으므로, 그냥 인트 타입으로 받는 것이 아니라 옵셔널 인트타입으로 스트림연산의
    	//결과물을 받은 뒤, 이프 엘스로 경우의 수 처리를 해 준다. 이때 옵셔널인트의 값이 있나, 없나는 옵셔널인트 객체
    	//에서 제공하는 isPresent()메서드를 사용하면 된다.
    	//최솟값을 찾고 싶다면, max() 부분을 min()으로 바꾸면 된다.
    	int[] intNum2 = {0,2,4};
    	OptionalInt maxOddNum = Arrays.stream(intNums).filter(x -> (x%2==1)).max();
    	if(maxOddNum.isPresent() != false) System.out.println(maxOddNum.getAsInt());
    	else System.out.println("NULL");
    	
    	OptionalInt maxOddNum2 = Arrays.stream(intNum2).filter(x -> (x%2==1)).max();
    	if(maxOddNum2.isPresent() != false) System.out.println(maxOddNum2.getAsInt());
    	else System.out.println("NULL");
    	
    	
    	//박싱된 타입의 배열 즉, Integer[]로 변환하여 반환하시오.
    	Integer[] intToIntegerArr = Arrays.stream(intNums).boxed().toArray(Integer[]::new);
    	System.out.println(
    			Arrays.toString(intToIntegerArr)
    			);
    	
    	
    	
    	
    	
    	
    	
    	
    	
    	System.out.println("\n\n\n\n\n***** 2차 배열과 2차 리스트 간의 상호 변환 테스트 시작!!");
    	int[][] twoDimentionalNums = {{0,1},{2,3},{4,5,99},{6,7},{8,9}};
    	
    	//2차 배열을 2차 리스트 형태로 바꾸시오.
    	List<List<Integer>> twoDimentionalNumsList = Arrays.stream(twoDimentionalNums).map(
    			arr -> Arrays.stream(arr).boxed().collect(Collectors.toList())
    			).collect(Collectors.toList());
    	for(List<Integer> elem : twoDimentionalNumsList) {
    		System.out.println(elem);
    	}
    	
    	//위에서 만들어냈던 2차 리스트를 다시 2차 배열로 바꾸시오.
    	int[][] twoDIntegerListToTwoDIntArr = twoDimentionalNumsList.stream().map(
    			list -> list.stream().mapToInt(x->x).toArray()
    			).toArray(int[][]::new);
    	for(int[] elem : twoDIntegerListToTwoDIntArr) {
    		System.out.println(Arrays.toString(elem));
    	}
    	
    	
    	
    	
    	
    	
    	
    	
    	
    	
    	
    	System.out.println("\n\n\n\n\n***** Integer 타입 리스트에서 스트림 사용법 테스트 시작!!!");
    	List<Integer> intList = Arrays.asList(56,3,-5,-57,1,75,4,-8,2,-3,6,0,-9,24,-6,8,-4,9,65,14);
    		
    		
    	//최댓값(최소값을 찾고 싶다면 max()를 min()으로 바꾸면 된다.)을 찾으시오. 단 최댓값을 찾을 수 없다면 예외를 던지시오.
    	int maxValInList = intList.stream().mapToInt(x -> x).max().orElseThrow(NoSuchElementException::new); 
    	System.out.println("최댓값 : " +
    			maxValInList
    			);
    	
    	//평균값을 찾으시오
    	double avgValInList = intList.stream().mapToInt(x -> x).average().orElseThrow(NoSuchElementException::new);
    	System.out.println("평균값 : " +
    			avgValInList
    			);
    	
    	//닫힌 구간 10~70 이내의 숫자들만 골라낸 후 오름차순으로 정렬하여 반환하시오.
    	Predicate<Integer> tenToSeventyInList = e -> ( 10 <= e && e <= 70);
    	System.out.println(
    			"10이상 70이하인 값들 모아서 오름차순 정렬 : " +
			intList.stream().sorted().filter(tenToSeventyInList).collect(Collectors.toList())
    			);
    			
    	
    	//위의 값들을 12와의 차이의 절댓값이 작은 순서대로 나열하시오.
    	//이때, 베이스 타입인 인트 타입으로는 sorted()메서드에 람다식으로 명시한 정렬
    	//규칙을 바로 적용할 수는 없으므로 boxed()를 중간에 끼워줘야 함.
    	System.out.println("12와의 차이의 절댓값이 작은 순서대로 나열 : " +
    			intList.stream().sorted(
    					(x,y) -> ( Math.abs(x-12) - Math.abs(y-12) )
    					).collect(Collectors.toList())
    			);
    	
    	//오름차순으로 정렬하시오
    	System.out.println("오름차순 정렬 : " +
 			intList.stream().sorted().collect(Collectors.toList())
    			);
    	
    	//내림차순으로 정렬하시오
    	//이때도 역시 내림차순 정렬기능을 제공하는 Collections.reverseOrder()가
    	//베이스 타입인 인트 타입을 인자로 받아들이지를 못해서 intNums 의 요소들을
    	//Integer라는 박스 타입(==wrapper type)으로 바꿔주는 boxed()메서드를
    	//써줘야 함.
    	System.out.println("내림차순 정렬 : " +
    					intList.stream().sorted(
    	    					Collections.reverseOrder()
    	    					).collect(Collectors.toList())
    			);
    	
    	//소수인 수를 찾으시오
    	System.out.println("소수 모음 : " +
    			intList.stream().filter( x -> isPrime(x)).collect(Collectors.toList())
    			);
    	
    	//소수가 아닌 수를 찾으시오
    	System.out.println("소수 아닌 수 모음 : " +
    			intList.stream().filter( x -> isPrime(x)==false).collect(Collectors.toList())
    			);
    	
    	//배열로 바꾸시오
    	int[] integerListToIntArr = intList.stream().mapToInt(x->x).toArray();
    	System.out.println("리스트를 배열로. : " +
    			Arrays.toString(integerListToIntArr)
    			);
 
    	
    	//홀수를 찾아서 리스트형태로 반환하시오.
    	List<Integer> oddNumsList = intList.stream().filter(
    			x -> (x%2 == 1)
    			).collect(Collectors.toList());
    	System.out.println(
    			"홀수만 모으기. : " +
    			oddNumsList
    			);
    	
    	//짝수를 찾아서 리스트 형태로 반환하시오.
    	List<Integer> evenNumsList = intList.stream().filter(
    			x -> (x%2 == 1)
    			).collect(Collectors.toList());
    	System.out.println(
    			"짝수만 모으기. : " +
    			evenNumsList
    			);
    	
    	
    	//홀수 중 최댓값을 찾으시오. 찾지 못한 경우에 대해서도 처리하시오.
    	//홀수가 하나도 없을 수도 있으므로, 그냥 인트 타입으로 받는 것이 아니라 옵셔널 인트타입으로 스트림연산의
    	//결과물을 받은 뒤, 이프 엘스로 경우의 수 처리를 해 준다. 이때 옵셔널인트의 값이 있나, 없나는 옵셔널인트 객체
    	//에서 제공하는 isPresent()메서드를 사용하면 된다.
    	//최솟값을 찾고 싶다면, max() 부분을 min()으로 바꾸면 된다.
    	List<Integer> intNumList2 = List.of(0,2,4);
    	OptionalInt maxOddNumInList = intList.stream().filter(x -> (x%2==1)).mapToInt(x->x).max();
    	if(maxOddNumInList.isPresent() != false) System.out.println(maxOddNumInList.getAsInt());
    	else System.out.println("NULL");
    	OptionalInt maxOddNumInList2 = intNumList2.stream().filter(x -> (x%2==1)).mapToInt(x->x).max();
    	if(maxOddNumInList2.isPresent() != false) System.out.println(maxOddNumInList2.getAsInt());
    	else System.out.println("NULL");
    	
    	
    	//박싱된 타입의 배열 즉, Integer[]로 변환하여 반환하시오.
    	Integer[] integerListToIntegerArr = intList.stream().toArray(Integer[]::new);
    	System.out.println(
    			Arrays.toString(integerListToIntegerArr)
    			);
    	
    	
    	
    	
    	System.out.println("\n\n\n\n\n***** 스트링 배열에 대한 스트림 기초 사용법 테스트 시작!!");
    	String[] colors = {"Red", "orange", "Yellow", "green", "Blue", "indigo", "Violet"};
    	
    	//전부 대문자로 바꾸시오.
    	//전부 소문자로 바꾸고 싶다면 String::toUpperCase를 String::toLowerCase로 바꾸면 된다.
    	System.out.println("전부 대문자로 바꾸기. : " +
    			Arrays.stream(colors).map(String::toUpperCase).collect(Collectors.toList())
    			);
    	
    	// 대소문자에 상관없이, 영소문자 m보다 나중에 등장하는 단어들을 사전순으로 정렬하여 반환하시오.
    	System.out.println("m보다 나중에 등장하는 단어들만 모아서 사전순 정렬 : " +
    			Arrays.stream(colors).filter(
    					s -> s.compareToIgnoreCase("n") > 0
    					).sorted(String.CASE_INSENSITIVE_ORDER).collect(Collectors.toList())
    			);
    	
    	// 대소문자에 상관없이, 영소문자 m보다 나중에 등장하는 단어들을 사전순의 역순으로 정렬하여 반환하시오.
    	//sorted() 내의 정렬 규칙에서 .toLowerCase()를 써주지 않으면, 소문자가 무조건 대문자보다 나중으로 배치되기 때문에
    	//이를 막고자 toLowerCase()를 이용해서 비교 전에 양측의 형식을 똑같이 맞춰준 것이다.
    	System.out.println("m보다 나중에 등장하는 단어들만 모아서 대소문자 무관하게 사전의 역순으로 정렬 : " +
    			Arrays.stream(colors).filter(
    					s -> s.compareToIgnoreCase("n") > 0
    					).sorted( 
    							(bf, af) -> af.toLowerCase().compareTo(bf.toLowerCase())
    							).collect(Collectors.toList())
    			);
      
      
    	//색깔 문자열들을 길이가 짧은 순서대로 정렬하되, 길이가 같을 경우 사전순으로 빠른 문자가 먼저 등장하게 하시오.
        // 정렬 규칙이 람다식 1줄만으로 정의 되기에는 복잡한 편이므로, 별도의 MySortRule 클래스를 정의하여
        // 스트림의 sorted()메서드에 파라미터로서 전달해 준다.
        System.out.println(
                Arrays.stream(colors).sorted(new MySortRule()).collect(Collectors.toList())
        );
      
      
      
      
      
      
    	
    	
    	
    	
    	System.out.println("\n\n\n\n\n***** 스트림을 활요하여 중첩된 맵을 초기화하는 방법 테스트 시작!!");
    	//이펙티브 자바 3판의 37번 아이템에서 등장하는 스트림 활용 예시다.
    	//물질의 상태 변이는 변이 이전과 변이 이후로 구성돼 있고, 이러한 변이 과정에는 나름의 고유한 이름이 붙어 있다.
    	//정리해 보면 아래와 같다.
    	//이전 상태:이후 상태  >>>  이러한 상태변이를 지징하는 이름 >>> enum Phase의 표시 내용
    	//    고체:액체      >>>  액화                      >>> MELT(SOLID, LIQUID)
		//    액체:고체      >>>  응고                      >>> FREEZE(LIQUID, SOLID)
		//    액체:기체      >>>  기화                      >>> BOIL(LIQUID, GAS)
		//    기체:액체      >>>  응축                      >>> CONDENSE(GAS, LIQUID)
		//    고체:기체      >>>  승화                      >>> SUBLIME(SOLID, GAS)
		//    기체:고체      >>>  승화                      >>> DEPOSIT(GAS, SOLID)
    	//    기체:플라즈마   >>>  이온화                     >>> IONIZE(GAS, PLASMA)
    	// 플라즈마:기체      >>>  탈이온화                   >>> DEIONIZE(PLASMA, GAS)
    	//아래의 코드와 같이 from() 메서드에 from(이전상태, 이후상태)와 같이 파라미터를 전달하면
    	//고체 >> 액체 로 변이하는 상태변화인 MELT를 리턴 받을 수 있도록 EnumMap을 스트림을 이용하여 구성하시오.
    	Transition phase = Transition.from(Phase.SOLID, Phase.LIQUID);
    	System.out.println(phase);//출력 결과 : MELT
    	System.out.println();
    	
    	//자세한 설명은 enum Phase 클래스 코드를 참고할 것.
    	System.out.println("바깥 맵의 키 들을 전부 출력해보자.");
    	for(Phase phaseName : Transition.transition2DMap.keySet()) {
    		System.out.println(phaseName);
    	}
    	System.out.println("바깥 맵의 키들을 바탕으로, 안쪽 맵들의 키들을 전부 찾아보자.");
    	for(Phase phaseName : Transition.transition2DMap.keySet()) {
    		System.out.println(Transition.transition2DMap.get(phaseName).keySet());
    	}
    	System.out.println("바깥 맵의 키들을 바탕으로, 안쪽 맵들의 값들을 전부 찾아보자.");
    	for(Phase phaseName : Transition.transition2DMap.keySet()) {
    		System.out.println(Transition.transition2DMap.get(phaseName).values());
    	}
    	
        
    }// main
    
    public static boolean isPrime(int n) {
    	if(n<2) return false;
    	return IntStream.rangeClosed(2, (int)Math.sqrt(n)).allMatch(x -> n % x != 0 );
    }
    
    
}// main class


class MySortRule implements Comparator<String>{
	public int compare(String bf, String af) {
		int result = bf.length() - af.length();
		if(result != 0) return result;
		else {
			return bf.toLowerCase().compareTo(af.toLowerCase());
		}
	}
}







//이펙티브 자바에서 등장한 코드들 중에서 가장 이해하기 까다로웠던 코드다.
enum Phase {
	
	//이놈들은 상태의 이름이다. 즉, 전이의 '결과'들이다.
	//플라즈마 상태를 추가하고 싶다면, 여기에 PLASMA를 추가하면 된다.
	SOLID, LIQUID, GAS;
	
	public enum Transition{
		//이놈들은 전이의 종류를 정리한 것이다.
		//액체와 고체 간의 전이는 2 종류가 있다. 고 >> 액 / 액 >> 고 이렇게.
		//액체와 기체, 기체과 고체도 마찬가지다.
		//플라즈마와 기체 간의 전이 2 종류를 추가하고 싶다면,
		//IONIZE(GAS, PLASMA)와 DEIONIZE(PLASMA, GAS) 를 추가해주면 된다.
		MELT(SOLID, LIQUID),
		FREEZE(LIQUID, SOLID),
		
		BOIL(LIQUID, GAS),
		CONDENSE(GAS, LIQUID),
		
		SUBLIME(SOLID, GAS),
		DEPOSIT(GAS, SOLID);
		
		private final Phase from;
		private final Phase to;
		
		Transition(Phase from, Phase to){
			this.from = from;
			this.to = to;
		}
		
		//이 코드의 작동방식을 이해하기 위해서는 이펙티브 자바의 저자(조슈아 블로크)의 의도를 먼저 이해해야 한다.
		//그러기 위해서는 이 코드를 주의 깊게 살펴볼 필요가 있다.
		/* 이놈들을 보면, 모든 전이(MELT, FREEZE 등)는 공통적으로 그 전이가 발생하기 위한 이전 상태와 이후 상태
		 * 가 있음을 알 수 있다.
		 전이(    이전상태, 이후상태)
		MELT(     SOLID, LIQUID),
		FREEZE(  LIQUID, SOLID),
		
		BOIL(    LIQUID, GAS),
		CONDENSE(   GAS, LIQUID),
		
		SUBLIME(  SOLID, GAS),
		DEPOSIT(    GAS, SOLID);
		
		이러한 상황에서 '이전상태'가 같은 것들끼리 묶어보자.
		그러면 아래와 같은 결과가 나올 것이다.
		
		MELT(     SOLID, LIQUID),
		SUBLIME(  SOLID, GAS),
		
		FREEZE(  LIQUID, SOLID),
		BOIL(    LIQUID, GAS),
		
		CONDENSE(   GAS, LIQUID),
		DEPOSIT(    GAS, SOLID);
		
		솔리드, 리퀴드, 가스 라는 3가지 이전 상태는 각각 2 가지의 이후 상태를 가지고 있음을 확인할 수 있을 것이다.
		// 그런다면, 
		 * 2차원 맵에서 솔리드, 리퀴드, 가스라는 3가지의 이전 상태를 키로 가지는 바깥 맵을 만들고,
		 * 솔리드, 리퀴드, 가스 라는 바깥맵 키들에 대해서 각각 1개의 안쪽 맵을 바깥 맵 키의 '값'으로서 매핑해주는 것이다.
		 * 그리고 이러한 안쪽 맵(총 3개다) 각각은 이후 상태 2개를 키로, 그리고 그 이후 상태에 맞는 이전 상태를 값으로 갖는 것이다.
         그림으로 정리해 보면 아래와 같다.
		 * 
   		 *        .-[바깥 맵]키          [바깥 맵]값
   		 *        |   ==이전상태           =={안쪽맵 인스턴스를 새로 만들어준다. 3개의 안쪽 맵은 각자 2개의 (키/값)쌍을 가지고 있는 것!!}
		 *        | 솔리드 --------->>  {안쪽 맵 0}---->(안쪽 맵의 키==이후 상태 : 리퀴드)&&(안쪽 맵의 값==전이 이름 : MELT)
		 *        |                              |-->(안쪽 맵의 키==이후 상태 : 가스 )&&(안쪽 맵의 값==전이 이름 : SUBLIME)
		 *        |                                  
transtion2DMap----|                                  
   ==[바깥 맵]    | 리퀴드 --------->>  {안쪽 맵 1}--->(안쪽 맵의 키==이후 상태 : 솔리드)&&(안쪽 맵의 값==전이 이름 : FREEZE)
		 *        |                              |-->(안쪽 맵의 키==이후 상태 : 가스)&&(안쪽 맵의 값==전이 이름 : BOIL)
		 *        |                                  
		 *        |                                  
         *        |_ 가스 ---------->>  {안쪽 맵 2}---->(안쪽 맵의 키==이후 상태 : 솔리드)&&(안쪽 맵의 값==전이 이름 : DEPOSIT)
		 *                                        |-->(안쪽 맵의 키==이후 상태 : 리퀴드)&&(안쪽 맵의 값==전이 이름 : CONDENSE)
		 * 
		
		 * */
		public static final Map<Phase, Map<Phase, Transition>> transition2DMap = 
				Stream.of(values()).collect(
						
						//이놈은 바깥 맵을 만들어주기 위한 것이다.
						Collectors.groupingBy(
								
								t -> t.from, () -> new EnumMap<>(Phase.class),
								
						//이놈은 바깥 맵이 가지게 될 솔리드, 리퀴드, 가스라는 키 3개에 대하여 각각 2개의 안쪽 맵 인스턴스를 만들고,
						// 각각의 안쪽맵 인스턴스들은 이후 상태를 키로, 전이 이름을 값으로 가지도록 맵핑하기 위한 것이다.
						//  Collectors.toMap(t->t.to, t -> t, (x,y) -> y, ()-> new EnumMap<>(Phase.class) ) 코드에서
						// t -> t.to 는 키 맵퍼이고, t -> t는 값 매퍼이다.
						// public enum Transition{...} 클래스의 시작 부분에서
						//MELT(SOLID, LIQUID) 와 같이 전이 이름과 그 전이 이름이 나오가 위한 이전 상태와 이후 상태를 짝지어 놓은 것을
						// 확인할 수 있을 것이다. 여기의 MELT가 t인 것이고, LIQUID가 t.to인 것이다.
						// (x,y) -> y 부분이 왜 필요한지에 대해서는 이펙티브 자바 3판 한국어판의 230쪽의 아래에서 10번째 줄에서
						// 잘 설명해주고 있으니 참고하면 될 것이다.
						//
						Collectors.toMap(t->t.to, t -> t, (x,y) -> y, ()-> new EnumMap<>(Phase.class) )
						
								)//groupingBy
						
						);//collect
		
		
		public static Transition from(Phase from, Phase to) {
			return transition2DMap.get(from).get(to);
		}
	}//end of Transition enum
	
}//end of enum
```
