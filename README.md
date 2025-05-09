[![PHP Version](https://img.shields.io/badge/PHP-7.3%2B-purple.svg)](https://www.php.net)
[![Laravel Version](https://img.shields.io/badge/Laravel-8.x-red.svg)](https://laravel.com)
[![Grafana Version](https://img.shields.io/badge/Grafana-8.x-orange.svg)](https://grafana.com)
[![Docker Version](https://img.shields.io/badge/Docker-20.10%2B-blue.svg)](https://www.docker.com)
[![Nginx Version](https://img.shields.io/badge/Nginx-1.21%2B-green.svg)](https://nginx.org)
[![Redis Version](https://img.shields.io/badge/Redis-6.x-red.svg)](https://redis.io)
[![Prometheus Version](https://img.shields.io/badge/Prometheus-2.x-yellow.svg)](https://prometheus.io)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

# Laravel Blog - Technical Documentation

## System Architecture

### Core Technologies
- **Framework**: Laravel 8.x [![Laravel Version](https://img.shields.io/badge/Laravel-8.x-red.svg)](https://laravel.com)
- **PHP Version**: 7.3+ [![PHP Version](https://img.shields.io/badge/PHP-7.3%2B-purple.svg)](https://www.php.net)
- **Cache & Queue System**: Redis [![Redis Version](https://img.shields.io/badge/Redis-6.x-red.svg)](https://redis.io)
- **Web Server**: Nginx [![Nginx Version](https://img.shields.io/badge/Nginx-1.21%2B-green.svg)](https://nginx.org)
- **Containerization**: Docker & Docker Compose [![Docker Version](https://img.shields.io/badge/Docker-20.10%2B-blue.svg)](https://www.docker.com)
- **Monitoring Stack**: Prometheus + Grafana [![Prometheus Version](https://img.shields.io/badge/Prometheus-2.x-yellow.svg)](https://prometheus.io) [![Grafana Version](https://img.shields.io/badge/Grafana-8.x-orange.svg)](https://grafana.com)

### Database Structure

#### Core Tables
| Table | Primary Key | Foreign Keys |
|-------|-------------|--------------|
| users | id | - |
| posts | id | user_id → users(id) |
| comments | id | user_id → users(id), post_id → posts(id) |
| categories | id | - |
| post_category | id | post_id → posts(id), category_id → categories(id) |
| tags | id | - |
| post_tag | id | post_id → posts(id), tag_id → tags(id) |

#### User Interaction
| Table | Primary Key | Foreign Keys |
|-------|-------------|--------------|
| post_user_likes | id | user_id → users(id), post_id → posts(id) |

#### Authentication & API
| Table | Primary Key | Foreign Keys |
|-------|-------------|--------------|
| personal_access_tokens | id | tokenable_id → users(id) |
| password_resets | id | email → users(email) |

#### Queue & Jobs
| Table | Primary Key | Foreign Keys |
|-------|-------------|--------------|
| jobs | id | - |
| failed_jobs | id | - |

#### Bot System
| Table | Primary Key | Foreign Keys |
|-------|-------------|--------------|
| bots | id | - |

#### Authentication & Authorization
| Table | Primary Key | Foreign Keys |
|-------|-------------|--------------|
| roles | id | - |
| user_role | id | user_id → users(id), role_id → roles(id) |
| permissions | id | - |
| role_permission | id | role_id → roles(id), permission_id → permissions(id) |

#### Media & Settings
| Table | Primary Key | Foreign Keys |
|-------|-------------|--------------|
| media | id | user_id → users(id) |
| settings | id | - |

#### Logging & Notifications
| Table | Primary Key | Foreign Keys |
|-------|-------------|--------------|
| logs | id | user_id → users(id) |
| notifications | id | user_id → users(id) |


### System Components

#### 1. Application Layer
- **Framework**: Laravel 8.x with MVC architecture
- **Authentication**: Laravel Sanctum for API authentication
- **CORS**: Fruitcake/Laravel-CORS for cross-origin resource sharing
- **Development Tools**: 
  - Laravel Tinker for REPL
  - Laravel Sail for Docker development
  - PHPUnit for testing

#### 2. Infrastructure Layer
- **Container Orchestration**: Docker Compose v3.8
- **Service Architecture**:
  - PHP-FPM Application Container
  - Nginx Web Server
  - Redis Cache/Queue
  - Prometheus Metrics Collector
  - Grafana Visualization

#### 3. Monitoring & Observability
- **Metrics Collection**: Prometheus
  - Custom metrics endpoints
  - Time-series data storage
- **Visualization**: Grafana
  - Custom dashboards
  - Real-time monitoring
  - Alert management

#### 4. Bot System Architecture
- **Command Pattern**: Laravel Artisan Commands
- **Service Layer**: BotService implementation
- **Queue Management**: Redis-backed job queues
- **Activity Simulation**: Automated user behavior patterns

## Technical Implementation Details

### 1. Container Configuration
```yaml
Services:
  - app: PHP-FPM Application
  - nginx: Web Server
  - redis: Cache/Queue
  - prometheus: Metrics
  - grafana: Visualization
```

### 2. Development Environment
- **PHP Extensions**: Custom configured in Dockerfile
- **Development Tools**: 
  - Composer for PHP dependencies
  - NPM for frontend assets
  - Laravel Mix for asset compilation

### 3. Performance Optimizations
- Redis caching layer
- Queue system for background jobs
- Asset compilation and optimization
- Database query optimization

### 4. Security Implementation
- Laravel Sanctum for API security
- CORS policy configuration
- Environment-based configuration
- Secure headers implementation

## Monitoring & Metrics

### Prometheus Integration
- Custom metrics endpoints
- System resource monitoring
- Application performance metrics
- Bot activity tracking

### Grafana Dashboards
- System health monitoring
- Application performance metrics
- Bot activity visualization
- Resource utilization tracking

## Development Workflow

### Local Development
1. Docker-based development environment
2. Hot-reload enabled for frontend
3. Automated testing setup
4. Development tools integration

### Deployment Pipeline
1. Container-based deployment
2. Environment configuration
3. Database migration handling
4. Asset compilation

## Technical Requirements

### System Requirements
- Docker Engine 20.10+
- Docker Compose 2.0+
- 4GB RAM minimum
- 20GB storage space

### Development Requirements
- PHP 7.3|8.0
- Node.js 14+
- Composer 2.0+
- Git

## Performance Considerations

### Caching Strategy
- Redis-based caching
- Query result caching
- View caching
- Route caching

### Queue Management
- Redis-backed queues
- Job batching
- Failed job handling
- Queue monitoring

## Security Measures

### Authentication
- Token-based authentication
- Session management
- CSRF protection
- Rate limiting

### Data Protection
- Environment-based configuration
- Secure headers
- Input validation
- XSS protection

## License

MIT License - See LICENSE file for details


