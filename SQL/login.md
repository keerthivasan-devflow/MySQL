
CREATE LOGIN kvasan WITH PASSWORD = "keerthi97"

CREATE USER test_user for LOGIN kvasan

GRANT SELECT ON employees to test_user