


1. 测试组件的事件
  ```js
  import SortByMenu from 'shared/components/SortByMenu';

      const sortMenu = component.find(SortByMenu);
      expect(sortMenu).toHaveLength(1);
      sortMenu.at(0).prop('onChange')(1);
  ```