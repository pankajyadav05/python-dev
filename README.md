# Python Developer Assessment

---

## Database Credentials

```
Host: [provided separately]
Port: 5432
Database: rules_engine_db
User: [provided separately]
Password: [provided separately]
```

---

## Schema

**rules**

- id, target_field, priority, condition_column, condition_operator, condition_value, action_type, action_value

**source_data**

- id, bom_level, factory_name, supplier_name, state, city, supplier_type

**transformed_data**

- id, source_id, field_name, resolved_value, rule_id

---

## Context

You're building a rules engine. Each source record is evaluated against rules to determine field values. Rules are evaluated by priority — first match wins.

---

## Tasks

### Part 1 — Rules Evaluator

Build a function that takes a source record and target field, returns the resolved value.

**Support these operators:**

- equals, not_equals, is_empty, is_not_empty

**Support these actions:**

- use_column → use value from specified column
- set_default → use hardcoded value

---

### Part 2 — API

| Method | Endpoint               | Description                         |
| ------ | ---------------------- | ----------------------------------- |
| POST   | `/process/{source_id}` | Transform one record, store results |
| GET    | `/results/{source_id}` | Get resolved fields for a record    |

---

## Sample Rules (in DB)

| priority | target_field  | condition      | action              |
| -------- | ------------- | -------------- | ------------------- |
| 1        | supplier_name | bom_level = 0  | use factory_name    |
| 2        | supplier_name | bom_level != 0 | use supplier_name   |
| 3        | location      | state is_empty | use city            |
| 4        | category      | (default)      | set "Manufacturing" |
