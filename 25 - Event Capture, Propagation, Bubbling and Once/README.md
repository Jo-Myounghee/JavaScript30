# 1. Event Bubbling

- 특정 element에서 event 발생 시, 상위 element로 이벤트가 전파(propagation)되어 가는 현상
- 예시
  - nestde div 태그가 있고 모든 div에 click이벤트가 붙어있으면, 최하위 div를 클릭하면 그 위에 있는 모든 상위 element들에 이벤트가 차례로 발생



# 2. Event Capture

- Event Bubbling과 반대방향으로 전파(propagation)하는 방식



# 3. event.stropPropagation()

- 가장 직접적으로 이벤트가 발생한 element 이외에 전파(propagation)를 멈추기 위한 함수



# 4. Event Delegation

- 하위 요소에 각각 이벤트를 붙이지 않고 상위 요소에서 하위 요소의 이벤트들을 제어하는 방식
- 예시
  - input 리스트가 향후 늘어나는 경우 미리 작성해둔 addEventListener로는 나중에 생성한 input list에는 붙어있지 않아 작동하지 않지만, li 태그의 상위 element에 EventListener를 붙여 놓으면, Event Bubbling 현상에 의해 자동으로 Event 감지 가능

# 5. once

- event handler가 한 번만 작동하고, 그 다음에는 addEventListener가 제거되어 더 이상 작동하지 않음



출처 : https://velog.io/@mementomori/25.-Event-Capture-Propagation-Bubbling-and-Once