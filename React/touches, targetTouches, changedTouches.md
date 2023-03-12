We have the following lists:

- `touches`: A list of information for every finger currently touching the screen
- `targetTouches`: Like touches, but is filtered to only the information for finger touches that started out within the same node
- `changedTouches`: A list of information for every finger involved in the event

To better understand what might be in these lists, let’s go over some examples quickly. They vary according to the following rules:

- When I put a finger down, all three lists will have the same information. It will be in `changedTouches` because putting the finger down is what caused the event
- When I put a second finger down, `touches` will have two items, one for each finger. `targetTouches` will have two items only if the finger was placed in the same node as the first finger. `changedTouches` will have the information related to the second finger, because it’s what caused the event
- If I put two fingers down at exactly the same time, it’s possible to have two items in `changedTouches`, one for each finger
- If I move my fingers, the only list that will change is `changedTouches` and will contain information related to as many fingers as have moved (at least one).
- When I lift a finger, it will be removed from `touches`, `targetTouches` and will appear in `changedTouches` since it’s what caused the event
- Removing my last finger will leave `touches` and `targetTouches` empty, and `changedTouches` will contain information for the last finger



기본적으로 changedTouches는 이벤트에 관여한 터치 객제를 저장하고 있음.