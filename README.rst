----------------------
django-dashboard-reuse
----------------------


Django-admin-tools-stats is a django application which power dashboard modules with customer stats and charts.

The goal of this project is to to interrogate quickly your Model data and provide reports and statistics graph simple to read, use on a Dashboard.


Installation
------------

Dashboard-resue is a django based application, so the major requirements are :

    - python >= 2.4
    - Apache / http server with WSGI modules
    - Django Framework >= 1.3
    - MySQL-python >= 1.2.3
    - python-dateutil >= 1.5
    - django-qsstats-magic >= 0.6.1
    - django-chart-tools >= 0.2.1
    - django-admin-tools


Configure
---------

- Configure ``admin_tools``
- Add ``admin_tools_stats`` & ``chart_tools`` into INSTALLED_APPS in settings.py::

    INSTALLED_APPS = (
        ...
        'admin_tools_stats',
        'chart_tools',
        ...)
        
- Add following code to dashboard.py::

    from admin_tools_stats.modules import DashboardCharts, get_active_graph

    # append an app list module for "Country_prefix"
    self.children.append(modules.AppList(
        _('Dashboard Stats Settings'),
        models=('admin_tools_stats.*', ),
    ))

    # Copy following code into your custom dashboard
    # append following code after recent actions module or
    # a link list module for "quick links"
    graph_list = get_active_graph()
    for i in graph_list:
        kwargs = {}
        kwargs['graph_key'] = i.graph_key
        if request.POST.get('select_box_'+i.graph_key):
            kwargs['select_box_'+i.graph_key] = request.POST['select_box_'+i.graph_key]


        self.children.append(DashboardCharts(**kwargs))

- Do ``manage.py syncdb``
- Open admin panel, Configure ``Dashboard Stats Criteria`` & ``Dashboard Stats respectively``


Screenshot
----------

.. image:: https://github.com/Star2Billing/django-admin-tools-stats/raw/master/django-admin-tools-stats/docs/source/_static/admin_dashboard.png


Support 
-------

Star2Billing S.L. (http://www.star2billing.com) offers consultancy including 
installation, training and customization 

Please email us at sales@star2billing.com for more information
