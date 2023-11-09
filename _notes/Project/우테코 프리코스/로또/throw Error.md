class App {
  async play() {
    let carNames;
    let totalRound;
    
    while (true) {
      try {
        carNames = await this.getCarNames();
        this.validateCarNames(carNames);
        break; // 유효하면 while 루프를 빠져나감
      } catch (error) {
        Console.error(error.message); // 에러 메시지 출력
      }
    }

    while (true) {
      try {
        totalRound = await this.getTotalRound();
        this.validateTotalRound(totalRound);
        break; // 유효하면 while 루프를 빠져나감
      } catch (error) {
        Console.error(error.message); // 에러 메시지 출력
      }
    }

    // 나머지 경주 진행 로직...
  }

  validateCarNames(carNames) {
    if (carNames.some(name => name.length === MIN_NAME || name.length > MAX_NAME)) {
      throw new Error("[ERROR] 이름은 1자 이상, 5자 이하만 가능합니다.");
    }
  }

  validateTotalRound(totalRound) {
    if (isNaN(totalRound) || totalRound <= MIN_ROUND || totalRound > MAX_ROUND) {
      throw new Error("[ERROR] 0과 9사이의 자연수만 입력 가능합니다.");
    }
  }
  
  // getCarNames와 getTotalRound 메서드는 그대로 유지...
}
