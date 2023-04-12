## snapshots test
  每当你想要确保你的UI不会有意外的改变，快照测试是非常有用的工具。

  ```shell
    # 重新生成快照文件
    jest --updateSnapshot
  ```


## Mock Functions
1. jest.fn()
2. .mock property
3. Mock Return Values
4. Mocking Modules
5. Mocking Partials
   ```js
    jest.mock('../foo-bar-baz', () => {
      const originalModule = jest.requireActual('../foo-bar-baz');

      //Mock the default export and named export 'foo'
      return {
        __esModule: true,
        ...originalModule,
        default: jest.fn(() => 'mocked baz'),
        foo: 'mocked foo',
      };
    });
   ```
6. Mock Implementations(这个理解还不到位)
   ```js
    const myMockFn = jest
      .fn(() => 'default')
      .mockImplementationOnce(() => 'first call')
      .mockImplementationOnce(() => 'second call');

    console.log(myMockFn(), myMockFn(), myMockFn(), myMockFn());
    // > 'first call', 'second call', 'default', 'default'
   ```

## mock系统


## mock example

```jsx
// 一些常用库的mock
import { fireEvent, screen, render, waitFor, act } from '@testing-library/react';
import '@testing-library/jest-dom';
import { ThemeProvider } from '@chakra-ui/react';
import activeTheme from '@payment/theme';
import { Formik, Form as FormikForm } from 'formik';

jest.mock('../../../store/history', () => ({
  unblockNavigation: jest.fn(),
  preventNavigation: jest.fn(),
}));

jest.mock('../../../index', () => ({
  store: {
    dispatch: jest.fn(),
  },
}));

jest.mock('@active/react-utils/i18n/useLocale', () => ({
  __esModule: true,
  default: () => ({
    i18n: (str: string) => str,
  }),
}));

const mockState = {
  newTerminal: {
    canAdd: false,
  },
  editTerminal: {
    printerSaved: false,
    printerInfo: {
      hasPrinter: false,
    },
    basicSaved: false,
  },
  agency: { selected: {} },
  terminal: {
    paymentMethodIsInvalid: false,
    glCodeResult: {
      glCodeList: [] as never,
      loading: false,
    },
  },
};

const mockFormikProps = {
  isSubmitting: false,
  submitForm: jest.fn(),
  initialValues: {
    name: '',
    locationGuid: '',
    locationName: '',
    paymentMethodsChecked: [] as string[],
    drawerSessionEnabled: true,
  },
  dirty: false,
  values: {
    journalEnabled: true,
  },
};

jest.mock('react-redux', () => ({
  ...(jest.requireActual('react-redux') as Record<string, unknown>),
  useSelector: (param: CallableFunction) => {
    return param(mockState);
  },
  useDispatch: () => jest.fn(),
}));

jest.mock('react-router-dom', () => ({
  ...(jest.requireActual('react-router-dom') as Record<string, unknown>),
  useParams: () => {
    return { itemGuid: '123' };
  },
}));

jest.mock('formik', () => ({
  ...(jest.requireActual('formik') as Record<string, unknown>),
  useFormikContext: () => {
    return mockFormikProps;
  },
}));

```

