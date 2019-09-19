# monorepos 🎉

### Install Repo
``` shell
npm -i -g yarn
git clone https://github.com/tadjohnston/monorepos.git
cd monorepos
```

### Install packages
``` shell
yarn add typescript react react-dom @types/react @types/react-dom
```

### tsconfig.json
``` js
{
  "compilerOptions": {
    "allowJs": false,
    "allowSyntheticDefaultImports": true,
    "checkJs": false,
    "composite": true,
    "declaration": true,
    "declarationMap": true,
    "esModuleInterop": true,
    "experimentalDecorators": true,
    "jsx": "react",
    "incremental": true,
    "module": "esnext",
    "moduleResolution": "node",
    "noEmit": false,
    "noImplicitAny": true,
    "noImplicitReturns": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "pretty": true,
    "sourceMap": true,
    "strict": true,
    "strictNullChecks": true,
    "target": "es5",
    "lib": [
      "dom",
      "esnext.asynciterable",
      "es2015",
      "es5",
      "es6"
    ]
  }
}
```

### lerna.json
``` js
{
  "lerna": "3.4.3",
  "npmClient": "yarn",
  "packages": [
    "packages/react-components",
    "packages/utils",
  ],
  "version": "independent",
  "useWorkspaces": true
}
```

### jest.config.base.js
``` js
module.exports = {
  preset: 'ts-jest',
  globals: {
    'ts-jest': {
      tsConfig: {
        allowJs: true
      }
    }
  },
  roots: [
    '<rootDir>/src'
  ],
  setupFiles: [
    'test/setup.ts'
  ],
  testMatch: [
    '**/*-test.ts?(x)',
  ],
  testEnvironment: 'node',
  transform: {
    '^.+\\.(t|j)sx?$': 'ts-jest',
    '^.+\\.graphql$': 'jest-transform-graphql'
  },

  collectCoverage: false,
  collectCoverageFrom: [
    '**/src/**/*.ts',
    '**/src/**/*.tsx',
    '!src/**/*-test.ts',
    '!src/**/*-test.tsx',
    '!build/**/*',
    '!**/__stories__/**',
    '!**/node_modules/**',
    '!**/index.ts',
    '!src/**/const.ts',
    '!src/**/*.d.ts'
  ],
  coverageDirectory: './coverage',
  testPathIgnorePatterns: [
    'node_modules',
    'build'
  ],
  verbose: true
}
```

### eslintrc.js
``` js
module.exports = {
  parser: '@typescript-eslint/parser',
  parserOptions: {
    project: './tsconfig.eslint.json',
    ecmaVersion: 2018,
    sourceType: 'module',
  },
  settings: {
    react: {
      version: 'detect',
    },
  },
  extends: [
    '@rentpath/eslint-config-rentpath',
    'plugin:monorepo/recommended',
    'plugin:@typescript-eslint/eslint-recommended',
    'plugin:@typescript-eslint/recommended',
    'plugin:@typescript-eslint/recommended-requiring-type-checking'
  ],
  env: {
    browser: true,
    node: true,
    es6: true,
    jest: true,
  },
  plugins: [
    'react',
    'jsx-a11y',
    'jest',
    '@typescript-eslint',
  ],
  settings: {
    'import/extensions': ['.ts', '.tsx', '.d.ts'],
    'import/resolver': {
      node: {
        paths: ['packages', 'test'],
        extensions: ['.js','.ts', '.tsx', '.d.ts', '.graphql'],
      },
    },
  },
  rules: {
    'import/no-cycle': [0, { maxDepth: 3 }],
    'sort-imports': [
      'error',
      {
        ignoreCase: true,
        ignoreDeclarationSort: true,
        ignoreMemberSort: false,
        memberSyntaxSortOrder: ['none', 'all', 'multiple', 'single'],
      },
    ],
    'sort-keys': 2,
    '@typescript-eslint/semi': 0,
    '@typescript-eslint/no-explicit-any': 0,
    '@typescript-eslint/indent': ['error', 2],
    '@typescript-eslint/member-delimiter-style': ['error', {
      multiline: {
        delimiter: 'comma',
      },
    }],
    '@typescript-eslint/explicit-member-accessibility': [0],
    '@typescript-eslint/explicit-function-return-type': [0],
    '@typescript-eslint/camelcase': [0],
    '@typescript-eslint/no-unused-vars': [
      'error',
      {
        argsIgnorePattern: '^_',
      },
    ],
    'react/prop-types': 'off',
    'max-len': ['error', {
      code: 100,
      ignoreStrings: true,
      ignoreComments: true,
      ignoreUrls: true,
      ignoreRegExpLiterals: true,
    }],
    'operator-linebreak': ['error', 'after', {
      overrides: {
        '?': 'before',
        ':': 'before',
      }
    }],
    'no-confusing-arrow': 'off',
    'implicit-arrow-linebreak': 'off',
    'react/jsx-one-expression-per-line': 'off',
    'object-curly-newline': ['error', {
      'ObjectExpression': { multiline: true, minProperties: 0, consistent: true },
      'ObjectPattern': { multiline: true, minProperties: 3, consistent: true },
      'ImportDeclaration': { multiline: true, minProperties: 3, consistent: true },
      'ExportDeclaration': { multiline: true, minProperties: 3, consistent: true },
    }],
    'comma-dangle': ['error', 'always-multiline'],
  }
}
```

### package.json
``` js
  "scripts": {
    "clean": "rm -rf build",
    "build": "yarn tsc -b",
    "build:watch": "yarn build -w",
    "test": "yarn jest",
    "test:watch": "yarn run test --watch"
  },
```

### tsconfig.eslint.json
``` js
{
  // extend your base config so you don't have to redefine your compilerOptions
  "extends": "./tsconfig.json",
  "include": [
    "**/*.ts",
    "**/*.tsx",
    "**/*.d.ts"
  ],
  "exclude": [
    "**/build",
    "**/*.graphql"
  ]
}
```
