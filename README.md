# IntelliJ-IDEA-file-template-CamelCase
Чтобы внутри шаблона использовать имя файла в CamelCase нужно добавить код преобразования в начале шаблона
```
#foreach( $str in $NAME.split("-") )
  #set( $str = $str.substring(0,1).toUpperCase() + $str.substring(1) )
  #set( $CamelCaseName = $CamelCaseName + $str )
#end
```
Далее использовать переменную 

```
function ${CamelCaseName} {}
```

## Чтобы создать комплексный шаблон нужно:
- Перейти в настройки **File/Settings**
- Выбрать **Editor/File and Code Template**
- Во кладке **Files** нажать "+"
- Создать основной файл шаблона
- Далее нашимая иконку, рядом с кнопкой "+" (Create Child Template File) создаём дочерние шаблоны

### Пример: 

Создан основной шаблон: Name: `React Componet Template`, Extension: `tsx`, File name: `${NAME}/${NAME}`
```
#set( $CamelCaseName = "" )

#foreach( $str in $NAME.split("-") )
  #set( $str = $str.substring(0,1).toUpperCase() + $str.substring(1) )
  #set( $CamelCaseName = $CamelCaseName + $str )
#end
import React from 'react';
import styles from './${NAME}.module.scss';

type ${CamelCaseName}Props = {};
export function ${CamelCaseName}({}: ${CamelCaseName}Props) {
    return (
        <></>
    );
}
```

Создан дочерний шаблон: File name: `${NAME}/index`, Extension: `ts`
```
export * from './${NAME}'
```

Создан дочерний шаблон: File name: `${NAME}/${NAME}.module.scss`, Extension: `scss`
```
.${NAME} {}
```
Например в директории components нам нужно создать компонент `BaseInput`
Получится следуюшая структура:
```
-- components
-- -- base-input
-- -- -- base-input.module.scss
-- -- -- base-input.tsx
-- -- -- index.ts
```

Чтобы выбрать шаблон нужно выделить нужную директорию и в пункте New выбрать созданный шаблон `React Componet Template`
