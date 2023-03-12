## 기본 리스트 

```react
import React, {useEffect, useState} from 'react';

const generateNames = (count) => {
    const temp = [];
    for(let i=0;i<=count;i++) temp.push(`Test Name- ${i}`)
    return temp;
}

const LongList = () => {
    const [names , setNames] = useState([])
    
    useEffect(() => {
        setNames(generateNames(1000));
    },[])
    
    return <> {names.map(name => <ListItem name={name}/>)} </>
}

const ListItem = ({name}) => {
    console.log(`rendered ${name}`)
    return <div> Name is: {name} </div>
}

export default LongList;
```



## Virtualized 된 리스트

```react
import React, {useEffect, useState} from 'react';
import {List, AutoSizer, CellMeasurerCache, CellMeasurer} from 'react-virtualized';

const LongList = () => {
    // SAME AS BEFORE
    const generateNames = (count) => {
        const temp = [];
        for(let i=0;i<=count;i++) temp.push(`Test Name- ${i}`)
        return temp;
    }

    const [names , setNames] = useState(generateNames(1000))
  
    const cache = new CellMeasurerCache({
        defaultWidth: 500,
        defaultHeight: 900,
    });

    //List의 자체 제공 props
    const renderRow = ({ index, key, style , parent }) => {
        return <CellMeasurer
            key={key}
            cache={cache}
            parent={parent}
            columnIndex={0}
            rowIndex={index}>

            <div style={style}>
              Name is: {names[index]}
            </div>
        </CellMeasurer>
    }

    return <div className={'list'} style={{height: "100px"}}>
        <AutoSizer>
            {({ width, height }) => {
                return <List
                    width={width}
                    height={height}
                    rowRenderer={renderRow}
                    rowCount={names.length}
                    rowHeight={cache.rowHeight}
                    deferredMeasurementCache={cache}
                />
            }}
        </AutoSizer>
    </div>
}

export default LongList;
```



# CellMeasurer

고차 컴포넌트이며 cell의 내부 컨텐츠를 사용자에게 보이지 않게끔 일시적으로 렌더링하여 width와 height를 측정한다. 

2개의 경우의 수가 존재한다.

fixed width => dynamic height

fixed height => dynamic width



<Prop Types>

cache : 타입으로는 CellMeasurerCache

children : 타입으로는 Element 아님 Function (props.children)

columnIndex : column을 0으로 주게되면 rowIndex로 측정

parent : Parent grid를 향한 reference를 줌

rowIndex : 측정되는 row의 index



### <기본 양식>

```react
function cellRenderer ({ columnIndex, key, parent, rowIndex, style }) {
  const content // Derive this from your data somehow

  return (
    <CellMeasurer
      cache={cache}
      columnIndex={columnIndex}
      key={key}
      parent={parent}
      rowIndex={rowIndex}
    >
      <div
        style={{
          ...style,
          height: 35,
          whiteSpace: 'nowrap'
        }}
      >
        {content}
      </div>
    </CellMeasurer>
  );
}
```





# CellMeasurerCache

Parent grid(고차 컴포넌트)와 공유될 cell content의 측정치를 저장함.



<Prop Types>

defaultHeight : 측정되지 않은 셀의 높이는 이 값을 parent에게 전달함.

defaultWidth : 측정되지 않은 셀의 넓이는 이 값을 parent에게 전달함.

fixedHeight : 고정 height값을 넘김.

fixedWidth : 고정 width값을 넘김.

minHeight : row의 최소높이를 정해서 넘김.

minWidth : column의 최소넓이를 정해서 넘김.



(참고사항)

`CellMeasurerCache` is not meant to measure cells that are both dynamic width *and* height. It would be inefficient to do so since the size of a row (or column) is equal to the largest cell within that row



CellMeasurerCache는 Cell의 다이나믹한 넓이 높이를 가진 content를 저장하기 위함이 아니다.



----

# List

가상화된 리스트. 즉 row의 집합을 render할 시에 사용되는 고차 컴포넌트.



<Prop Types>

width : 리스트의 넓이

height : 실제로 리스트안에서 보여질 row의 개수를 컨트롤하는 리스트 높이

rowCount : 전체 row의 개수

rowHeight : row의 높이를 지정

rowRenderer : row를 1개 생성하는데 필요한 함수





# AutoSizer

```
부모 element의 너비와 높이를 자식 컴포넌트에 전달해주는 HOC이다. 이걸 활용하면 부모의 너비와 높이만큼 자식을 꽉 채울 수 있음.
```

![image-20220721222448983](md-images/image-20220721222448983-16584098899461.png)



부모 element의 너비와 높이를 받아서 single child를 자동으로 동일하게 조절해주는 HOC이다.





# 예외사항

List 컴포넌트의 height가 0일시에 내부 row들은 렌더링되지 않는다.



