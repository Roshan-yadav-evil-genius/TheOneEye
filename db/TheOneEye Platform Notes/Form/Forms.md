# Class Relationships

```mermaid
graph TB
    %% External Dependencies
    DjangoForms["django.forms<br/>(External)"]
    ABC["abc.ABC<br/>(External)"]
    
    %% Core Classes
    BaseForm["BaseForm<br/>- Core form functionality<br/>- Field value management<br/>- Form validation<br/>- Form rebinding"]
    DependentForm["DependentForm<br/>- Extends BaseForm<br/>- Adds dependency support<br/>- Cascading dropdowns"]
    FieldDependencyHandler["FieldDependencyHandler<br/>- Manages dependency cascading<br/>- Initializes dependencies<br/>- Handles field changes"]
    FieldDependencyProvider["FieldDependencyProvider<br/>- Abstract interface<br/>- get_field_dependencies()<br/>- populate_field()"]
    FormSerializer["FormSerializer<br/>- Serializes forms to JSON<br/>- Extracts field metadata<br/>- Handles async choices"]
    JSONTextareaWidget["JSONTextareaWidget<br/>- Custom textarea widget<br/>- JSON mode indicator"]
    
    %% Inheritance Relationships
    DjangoForms -->|inherits| BaseForm
    BaseForm -->|inherits| DependentForm
    FieldDependencyProvider -->|mixin| DependentForm
    DjangoForms -->|inherits| JSONTextareaWidget
    
    %% Composition/Usage Relationships
    DependentForm -->|creates instance| FieldDependencyHandler
    FieldDependencyHandler -.->|uses TYPE_CHECKING| BaseForm
    DependentForm -->|implements| FieldDependencyProvider
    
    %% Serialization Relationships
    FormSerializer -->|accepts any form| BaseForm
    FormSerializer -->|accepts| DependentForm
    FormSerializer -->|detects widget| JSONTextareaWidget
    
    %% External Usage (shown as notes)
    FormLoader["FormLoader<br/>(core/views/services)"]
    NodeExecutor["NodeExecutor<br/>(core/views/services)"]
    NodeForms["Node Forms<br/>(Various Nodes)"]
    
    FormLoader -->|uses| FormSerializer
    NodeExecutor -->|uses| FormSerializer
    NodeForms -->|inherit from| BaseForm
    NodeForms -->|inherit from| DependentForm
    
    %% Styling
    classDef baseClass fill:#e1f5ff,stroke:#01579b,stroke-width:2px
    classDef dependentClass fill:#fff3e0,stroke:#e65100,stroke-width:2px
    classDef handlerClass fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    classDef interfaceClass fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px
    classDef serializerClass fill:#fce4ec,stroke:#880e4f,stroke-width:2px
    classDef widgetClass fill:#fff9c4,stroke:#f57f17,stroke-width:2px
    classDef externalClass fill:#f5f5f5,stroke:#616161,stroke-width:1px,stroke-dasharray: 5 5
    
    class BaseForm baseClass
    class DependentForm dependentClass
    class FieldDependencyHandler handlerClass
    class FieldDependencyProvider interfaceClass
    class FormSerializer serializerClass
    class JSONTextareaWidget widgetClass
    class DjangoForms,ABC,FormLoader,NodeExecutor,NodeForms externalClass
```

- **Metaclass:** Metaclasses are classes for classes. Just as a class defines how objects behave, a metaclass defines how a class itself is created and behaves.

- `from django.forms.forms import DeclarativeFieldsMetaclass`  :  Without this metaclass, Django forms **would not know which attributes are fields**. In short: **This metaclass turns class attributes into form fields.**

  ### Its core job

  When you write:

  ```python
  class MyForm(forms.Form):
      name = forms.CharField()
      age = forms.IntegerField()
  ```

  `DeclarativeFieldsMetaclass`:

  1. **Intercepts class creation**

  2. Finds all class attributes that are instances of `Field`

  3. Removes them from the class namespace

  4. Collects them into:

     ```python
     MyForm.base_fields
     ```

  5. Preserves **field declaration order**

  6. Handles inheritance (parent form fields + child fields)

     

- `from abc import ABCMeta` : It enforces **abstract methods**

  

- ```python
  class FormABCMeta(DeclarativeFieldsMetaclass, ABCMeta):
      """Metaclass that combines Django's form metaclass with ABCMeta."""
      pass
  ```

  `FormABCMeta` This creates a **hybrid metaclass** that does **both**:

  | Feature                  | Provided by                  |
  | ------------------------ | ---------------------------- |
  | Collect form fields      | `DeclarativeFieldsMetaclass` |
  | Enforce abstract methods | `ABCMeta`                    |

  

- ## What does this enable in practice?

  It allows you to define **abstract Django forms**.

  ### Example usage

  ```python
  from abc import abstractmethod
  from django import forms
  
  class BaseForm(forms.Form, metaclass=FormABCMeta):
  
      name = forms.CharField()
  
      @abstractmethod
      def save(self):
          pass
  ```

  Now:

  ```python
  BaseForm()  
  # ❌ TypeError: Can't instantiate abstract class BaseForm
  ```

  ### Correct subclass

  ```python
  class UserForm(BaseForm):
  
      email = forms.EmailField()
  
      def save(self):
          print("Saving user")
  UserForm()  
  # ✅ Works
  ```

