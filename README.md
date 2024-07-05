# ¿Como configurar correctamente ESLint y prettier en un proyecto de next JS?
### En nuestra terminal hacemos lo siguiente 
```bash
rm -r .eslintrc.json
pnpx eslint --init
pnpm i -D eslint-plugin-prettier@4.0.0
pnpm i -D prettier prettier-plugin-tailwindcss
touch .prettierrc
```
### En el archivo **.prettierrc** añadimos lo siguiente
```json
{
  "plugins": ["prettier-plugin-tailwindcss"]
}
```
### Tu archivo de configuración de ESLint debería verse algo así (**eslint.config.mjs**)

```js
import globals from "globals";
import tseslint from "typescript-eslint";
import pluginReactConfig from "eslint-plugin-react/configs/recommended.js";
//Importamos dependencias de prettier
import prettierConfig from "eslint-config-prettier";  
import prettierPlugin from "eslint-plugin-prettier"; 

export default [
  {files: ["**/*.{js,mjs,cjs,ts,jsx,tsx}"]},
  { languageOptions: { parserOptions: { ecmaFeatures: { jsx: true } } } },
  {languageOptions: { globals: globals.browser }},
  ...tseslint.configs.recommended,
  // Añadimos dependencias de prettier a configuración de ESLint
  prettierConfig,
  prettierPlugin,
  pluginReactConfig,{
  	//Añadimos estas reglas a la configuración
    rules: {
      ...prettierConfig.rules,
      "react/react-in-jsx-scope": "off",
      "prettier/prettier": "error "
    }
  }
];
```

## Recuerda tener las extensiones de ESLint y prettier instaladas en vscode


