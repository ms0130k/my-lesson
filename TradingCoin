import java.util.Scanner;

//특이하게 주니코인은 가입시 10개의 코인을 무료제공하고, 현준이를 포함한 총 5명(0~4번, 현준이는 4번)의 사람만이 하루에 딱 한 번 순서대로 코인을 사거나 팔 수 있다.
//주니코인은 누군가 코인을 구매하면 구매한 수량만큼 즉시 가치가 올라가고, 판매하면 판매한 수량만큼 즉시 가치가 떨어지게 된다.  코인 판매금은 자본금으로 전환된다.
//(ex. 코인가치 10일 때  0번 사람이 코인 5개를 구매하면 코인가치는 10+5=15가 됨, 1번 사람이 거래할 때는 개당 15원으로 거래해야 함)
//
//단, 다음과 같은 경우에는 거래가 무효가 된다. 
//1. 구매시, 자본금이 부족한 경우
//2. 판매시, 판매하려는 코인 수 보다 보유한 코인 수가 작은 경우
//3. 구매나 판매시, 코인 가치가 음수가 되는 경우
//* 2021-05-11 16:41, 문제를 단순화하기 위해 2, 3번 추가
//
//3일 뒤 현준이의 코인 갯수와 주니 코인의 가치는 얼마인지 계산해보자.

//입력 설명
//100    # 현재 코인의 가치 (모든 입력값은 양의 정수)
//200 300 400 100 500    # 0~4번 사람의 초기 자본금 
//0 1 2      # (입력순서: 사람번호 구매or판매 수량), 1일차 - 0번 사람, 구매 2개 
//1 1 5      # 1번 사람, 구매, 5개
//2 2 5      # 2번 사람, 판매, 5개
//3 1 10    # 3번 사람, 구매, 10개
//4 2 3      # 4번 사람 = 현준, 판매, 3개
//0 1 2      # 2일차 - 각 사람의 구매 또는 판매 수량
//1 1 5 
//2 2 5 
//3 1 10
//4 1 5 
//0 1 2      # 3일차 - 각 사람의 구매 또는 판매 수량
//1 1 5 
//2 2 5 
//3 1 10
//4 1 3

//출력 설명
//x y     # x = 현준이의 코인 갯수, y = 코인 가치

class CoinTrading {
	static int currentPrice = 0;
}

class Person {
	int totalMoney;
	int totalCountOfCoin;
	
	public Person(int totalMoney) {
		this.totalMoney = totalMoney;
		this.totalCountOfCoin = 10;
	}
	
	public void buyCoin(int count) {
		System.out.println("거래이전 >> 잔액: " + this.totalMoney + ", 보유코인수: " + this.totalCountOfCoin);
		int requiredMoney = count * CoinTrading.currentPrice;
		int expectedCoinPrice = CoinTrading.currentPrice + count;
		
		if (requiredMoney > totalMoney || expectedCoinPrice < 0) {
			System.out.println("잔액부족 >> 잔액: " + this.totalMoney + ", 필요금액: " + requiredMoney);
			return;
		}
		
		CoinTrading.currentPrice = expectedCoinPrice;
		this.totalCountOfCoin += count;
		this.totalMoney -= requiredMoney;
		System.out.println("구매완료 >> 잔액: " + this.totalMoney + ", 보유코인수: " + this.totalCountOfCoin + ", 코인가격: " + expectedCoinPrice);
	}
	
	public void sellCoin(int count) {
		System.out.println("거래이전 >> 잔액: " + this.totalMoney + ", 보유코인수: " + this.totalCountOfCoin);
		int expectedCoinPrice = CoinTrading.currentPrice - count;
		
		if (expectedCoinPrice < 0) {
			System.out.println("가격에러 >> 현재코인 가격: " + CoinTrading.currentPrice + ", 거래성립시 가격: " + expectedCoinPrice);
			return;
		}
		if (totalCountOfCoin < count) {
			System.out.println("개수에러 >> 현재코인 개수: " + this.totalCountOfCoin + ", 구매하려는 코인 개수: " + count);
			return;
		}
		
		CoinTrading.currentPrice = expectedCoinPrice;
		this.totalCountOfCoin -= count;
		this.totalMoney += count * CoinTrading.currentPrice;
		System.out.println("판매완료 >> 잔액: " + this.totalMoney + ", 보유코인수: " + this.totalCountOfCoin + ", 코인가격: " + expectedCoinPrice);
	}
}

public class Main_Test {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		final int TYPE_BUY = 1;
		final int TYPE_SELL = 2;
		Person[] traders = new Person[5];
		
		System.out.println("코인 초기값을 입력하세요.");
		CoinTrading.currentPrice = sc.nextInt();
		System.out.println("인원별 금액을 입력하세요.");
		for (int i = 0; i < 5; i++) {
			System.out.print(i + "번 인원: ");
			int initialMoney = sc.nextInt();
			traders[i] = new Person(initialMoney);
		}
		
		for (int i = 0; i < 15; i++) {
			System.out.print("거래한 사람의 번호를 입력하세요: ");
			int personNum = sc.nextInt();
			System.out.print("거래유형을 입력하세요(1: 구매, 2: 판매): ");
			int tradingType = sc.nextInt();
			System.out.print("거래개수를 입력하세요: ");
			int count = sc.nextInt();
			if (tradingType == TYPE_BUY) {
				traders[personNum].buyCoin(count);
			} else if (tradingType == TYPE_SELL) {
				traders[personNum].sellCoin(count);
			} else {
				System.out.println("거래 방식이 잘못 입력되었습니다.");
			}
		}
		System.out.println("현준이 코인 개수: " + traders[4].totalCountOfCoin);
		System.out.println("코인가치: " + CoinTrading.currentPrice);
	}
}
