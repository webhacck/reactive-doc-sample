# サンプル

```@input
{
  "type": "text",
  "label": "エンドポイント",
  "defaultValue": "https://api.github.com/search/repositories",
  "variableName": "endpoint"
}
```

```@input
{
  "type": "text",
  "label": "パラメータ",
  "defaultValue": "?q=",
  "variableName": "param"
}
```

```@input
{
  "type": "text",
  "label": "キーワード",
  "defaultValue": "",
  "variableName": "key",
  "onChange": "init()"
}
```

<br/>

## コード例＆実行結果

```@template
{{endpoint}}{{param}}{{key}}
```

```@input
{
  "type": "button",
  "label": "実行する",
  "trigger": "getResult()"
}
```

```@code
function init() {
    const endpoint = 'https://api.github.com/search/repositories';
    const param = '?q=';

    setState('endpoint', endpoint);
    setState('param', param);
}

function getResult() {
    const url = `${getState('endpoint')}${getState('param')}${getState('key')}`;
    
    fetch(url)
    .then(data => data.json())
    .then(json => {
        setState('endpoint', '');
        setState('param', '');
        setState('key', `${getState('key')}のリポジトリ総数：${json.total_count}`);
    })
}
```
