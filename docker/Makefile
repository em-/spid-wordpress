up:
	docker-compose up -d
	composer install --no-interaction
	docker-compose run --rm wp-cli core install --title="SPID WP" --admin_user=test --admin_password=test --admin_email="test@example.com" --url=localhost --skip-email
	docker-compose run --rm wp-cli plugin activate spid-wordpress
	wget --timeout=15 --retry-connrefused -O docker/idp_conf/sp_metadata.xml "http://localhost/wp-login.php?sso=spid&metadata" # broken
	wget --timeout=15 --retry-connrefused -O docker/sp_conf/idp_metadata/testenv2.xml "http://localhost:8088/metadata"
	docker-compose restart

clean:
	rm -f docker/idp_conf/sp_metadata.xml
	rm -f docker/sp_conf/idp_metadata/testenv2.xml

.PHONY: up clean
