Create New Module
====================

New Module
-------------------------
Firstly git clone and install. Adding a simple new module includes:
* New schema and database Router script configuration
* startapp <new application>
* build data models and views based on utils.py in apputil, config urls and create templates

New schema and database Roter
-------------------------------
1. Add new application to routers.py in core:

  .. code-block:: python
      
        route_app_labels = {
        'default': {'auth', 'contenttypes','apputil'},
        ...,
        # here add new 
        # 'schema':{'newapplication'}
        }

2. In settings.py database config, adding:

.. code-block:: python
      
        DATABASES = {
            #...,
            'new schema': {
                # config as above.
                },
    },


Start with New Application
-------------------------------

.. code-block:: python
      
        manage.py startapp <new>

Building
----------
1. Add new model in models.py:

  .. code-block:: python
    
    #Import third package
    #Import django build in package
    #Import coadd package 
    from adjcoadd.constants import *
    from apputil.models import AuditModel, Dictionary


        class newmodel(AuditModel):
            #here create attribute: HEADER_FIELDS, CARD_FIELDS, FORM_GROUPS and others
            #here model fields
            #model meta
            #model methods

2. new modelform, filterform in forms.py:

  .. code-block:: python
    
    #Import third package
    #Import django build in package
    #Import coadd package 
    from apputil.models import Dictionary, ApplicationUser
    from apputil.utils.filters_base import Filterbase


        class newmodel_form(forms.ModelForm):
            #here formfields
            #form init method and other methods
            #form meta

        class newmodel_filter(Filterbase):
            #here filterfields
            #form init method and other methods
            #form meta

3. Add view class in views.py:
  
  .. code-block:: python

    #Import third package
    #Import django build in package
    #Import coadd package 
    from adjcoadd.constants import *
    from apputil.utils.filters_base import FilteredListView
    from apputil.utils.views_base import SimplecreateView, SimpleupdateView,HtmxupdateView, SimpledeleteView
    from .models import *
    from .forms import *

        # list view
        class Modellistview(FilteredListView):
            #here define view attribute:
            #login_url, model, template_name, filterset_class, model_fields, app_name, model_name and others            
            #or customize view methods:
            #get_queryset, get_context_data, get_paginate_by, get_order_by
        
        #detailview
        def modeldetail(request, pk):
            # set and return render context in template

        # create view
        class Modelcreateview(SimplecreateView):
            #here define view attribute: form_class, template_name, transaction_use            
            #or customize view methods
        
        # update view
        class Modelupdateview(SimpleupdateView or HtmxupdateView):
            #here define view attribute: form_class, template_name,template_partial(if use HtmxupdateView), model, transaction_use             
            #or customize view methods
        
        # delete view
        class Modeldeleteview(SimpledeleteView):
            #here define view attribute: model, transaction_use
            #or customize view methods       

4. config urls in urls.py:

  * in core(adjcoadd)/urls.py
  
  .. code-block:: python
    
    path('<new application>/', include('<new application.urls>')),

  * in new application/urls.py
  
  .. code-block:: python
    
    path('<modelname_list>/', Viewclass.as_view(), name="modelname_list"),
    path('<modelname_detail>/<str:pk>', viewfunction, name="modelname_detail"),
    path('<createmodel>/', Viewclass.as_view(), name="...create"),
    path('<update...>/<str:pk>', Viewclass.as_view(), name="...update"),
    path('<delete...>/<str:pk>', Viewclass.as_view(), name="...delete"),


5. templates:

  * in new application/templates/new application/model create:

    - model_c.html includes 'utils/modal/modal_form.html' and {% url 'model_create' as createurl %}
    - model_u.html includes update url, form with including {%include 'utils/row_editabletable.html' with form_label=field.label data_type=field.label form_field=field %}
    - model_d.html includes:
    
      * {%include 'utils/miscellaneous/delete_btn.html' with target='#model_detail_del'%},
      * {% include 'utils/modal/delete.html' with title='Delete Organism' deleteurl=deleteurl entry=object %} with delete url 
    
    - model_list.html includes:

      * {% url 'pivoted-table' app_model='applicationname-Modelname' as url_pivotedtable%}
      * {% include 'utils/leftbar.html'  with list_url='model_list' card_url='model_card' create_object='createModelname' create_objectModal='createModelnameModal' url_pivotedtable=url_pivotedtable %}
      * {% include "utils/sidebar.html" %}
      * {% include 'utils/main_horizalbar.html' with title='Modelname'  model_name='Modelname' application='applicationname' %}
      * {% include 'utils/datatable_general.html' with modelname='Modelname' %}

    - model_detail.html includes:  

      * {% include 'utils/lefticons.html' with title="Model" %}
      * {% include 'utils/message.html' %}
      * {% include './model_u.html' %}
             

    
