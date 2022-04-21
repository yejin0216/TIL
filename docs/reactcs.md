# React Cheet Sheet

## select input

```javascript
const select = ({ value, callback, selected }) => {
  return (
    <select
      disabled={disabled}
      readOnly={readonly}
      defaultValue={selected}
      onchange={({ target: { value } }) => callback(value)}
    >
      {values.map(([value, text]) => {
        <option value={value}>{text}</option>;
      })}
    </select>
  );
};
```
