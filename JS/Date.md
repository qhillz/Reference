# date

new Date(year, month, date, hours, minutes, seconds, ms)

- 주어진 인수를 조합해 만들 수 있는 날짜가 저장된 객체가 반환됩니다(지역 시간대 기준). 
  - 첫 번째와 두 번째 인수만 필수값입니다.

- year는 반드시 네 자리 숫자여야 합니다. 2013은 괜찮고 98은 괜찮지 않습니다.

- month는 0(1월)부터 11(12월) 사이의 숫자여야 합니다.

- date는 일을 나타내는데, 값이 없는 경우엔 1일로 처리됩니다.

- hours/minutes/seconds/ms에 값이 없는 경우엔 0으로 처리됩니다.

