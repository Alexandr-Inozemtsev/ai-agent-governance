# Trello Card Policy Example

## Обязательные поля карточки

- owner;
- labels;
- acceptance criteria;
- definition of done;
- dependencies;
- parent epic/task для bug cards;
- linked PR/test case при наличии.

## Правила движения

- В `Готово к разработке` можно двигать только при наличии acceptance criteria.
- В `Готово` можно двигать только после QA/Review.
- Epic нельзя закрывать при открытых P0/P1/Critical/High bugs.
- Duplicate card не создается: обновляется существующая.
