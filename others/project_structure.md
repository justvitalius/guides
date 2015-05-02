# Структура папок и файлов в проекте
- Выделяйте каждый конечный кусок кода в отдельный файл. И внутри каждого файла следуйте принципу `IIFE`.
- Если существует несколько файлов для реализации одного модуля, то помещайте его в папку с названием модуля
- Все файлы должны иметь суффикс. Например:
1. _factory
1. _service
1. _store
1. _view
1. _directive
1. _module


```
// хорошо
bower_components/
javascripts/
    app_module.js
    app_config.js
    app_routes.js
    app_dispatcher.js
    base/
        local_routes.js
        api_routes.js
        localstorage.js
    layout/
        topnav_directive.js
        topnav_controller.js
        user_profile_directive.js    
    components/
        calendar_directive.js
        bootstrap_input_directive.js
        timesheet_directive.js
    react_components/
        timesheet/
            timesheet_view.js
            timesheet_cell.js
            timesheet_row.js
    dashboard/
        dashboard_test_controller.js
        dashboard_navigtaion_directive.js
    facrories/
        mypermissions_factory.js
        permissions_factory.js
        logger_factory.js
        tariffs_api_factory.js
    helpers
        timesheet_helper.js
        row_render_helper.js
    employees/
        employees_module.js
        employees_factory.js
        employees_controller.js
        employee_actions.js
        employee_profile_controller.js
    

```