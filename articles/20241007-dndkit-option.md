---
title: "[dndkit] ドラック要素のドラックとクリックを使い分ける"
emoji: "♠️"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [dndkit, React]
published: false
---

## はじめに

この記事では、dndkit を用いてドロップ要素へドラックで移動できた Item へ、新たにクリックイベントを追加する方法を紹介しています。

## 改善前

- [] 挙動のgifを貼り付ける
- [] 下のソースは書き換えよう
```
return (
    <DndContext onDragEnd={handleDragEnd} sensors={sensors}>
      <SortableContext items={state}>
        {state.map((item, index) => (
          <SortableItem
            key={item.id}
            id={item.id}
            imgSrc={item.content}
            index={index}
          />
        ))}
      </SortableContext>
    </DndContext>
  );
```

## 改善後
dnd反映エリアは、DndContextタグでラップする必要があります。
DndContextは、sensorを受け取ることができます。sensorとして渡しているプロパティは、以下です。
```
const mouseSensor = useSensor(MouseSensor, {
    activationConstraint: {
      distance: 5,
    },
  });
  const keyboardSensor = useSensor(KeyboardSensor);
  const sensors = useSensors(mouseSensor, keyboardSensor);
```


- [参考:dnd kit でソート可能アイテム内にボタンがある時にボタンのクリックとアイテムのソートを両方できるようにする](https://www.gaji.jp/blog/2022/03/10/9281/)
- [公式ドキュメント](https://docs.dndkit.com/api-documentation/sensors#hooks)