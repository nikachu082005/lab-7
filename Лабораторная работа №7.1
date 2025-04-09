#include <iostream>
#include <fstream>
#include <vector>
#include <memory>
#include <stdexcept>

class Entity {
protected:
    std::string name;
    int health;
    int attack;
    int defense;

public:
    Entity(const std::string& n, int h, int a, int d)
        : name(n), health(h), attack(a), defense(d) {}
    virtual ~Entity() {}

    virtual void displayInfo() const = 0;
    virtual std::string getType() const = 0;

    // Методы для доступа к полям
    std::string getName() const { return name; }
    int getHealth() const { return health; }
    int getAttack() const { return attack; }
    int getDefense() const { return defense; }

    // Виртуальные методы для сохранения/загрузки
    virtual void save(std::ofstream& file) const {
        file << getType() << "\n";
        file << name << "\n";
        file << health << " " << attack << " " << defense << "\n";
    }

    virtual void load(std::ifstream& file) {
        std::getline(file, name);
        file >> health >> attack >> defense;
        file.ignore(); // Пропустить символ новой строки
    }
};

class Player : public Entity {
    int experience;

public:
    Player(const std::string& n, int h, int a, int d, int exp = 0)
        : Entity(n, h, a, d), experience(exp) {}

    std::string getType() const override { return "Player"; }

    void displayInfo() const override {
        std::cout << "Player: " << name << ", HP: " << health
                  << ", Attack: " << attack << ", Defense: " << defense
                  << ", Exp: " << experience << std::endl;
    }

    void save(std::ofstream& file) const override {
        Entity::save(file);
        file << experience << "\n";
    }

    void load(std::ifstream& file) override {
        Entity::load(file);
        file >> experience;
        file.ignore();
    }
};

class Enemy : public Entity {
    std::string type;

public:
    Enemy(const std::string& n, int h, int a, int d, const std::string& t)
        : Entity(n, h, a, d), type(t) {}

    std::string getType() const override { return "Enemy"; }

    void displayInfo() const override {
        std::cout << "Enemy: " << name << ", HP: " << health
                  << ", Attack: " << attack << ", Defense: " << defense
                  << ", Type: " << type << std::endl;
    }

    void save(std::ofstream& file) const override {
        Entity::save(file);
        file << type << "\n";
    }

    void load(std::ifstream& file) override {
        Entity::load(file);
        std::getline(file, type);
    }
};

template <typename T>
class GameManager {
private:
    std::vector<std::unique_ptr<T>> entities;

public:
    void addEntity(T* entity) {
        entities.emplace_back(entity);
    }

    void displayAll() const {
        for (const auto& entity : entities) {
            entity->displayInfo();
        }
    }

    void saveToFile(const std::string& filename) const {
        std::ofstream file(filename);
        if (!file) {
            throw std::runtime_error("Failed to open file for writing");
        }

        file << entities.size() << "\n";
        for (const auto& entity : entities) {
            entity->save(file);
        }
    }

    void loadFromFile(const std::string& filename) {
        std::ifstream file(filename);
        if (!file) {
            throw std::runtime_error("Failed to open file for reading");
        }

        entities.clear();
        int count;
        file >> count;
        file.ignore();

        for (int i = 0; i < count; ++i) {
            std::string type;
            std::getline(file, type);

            std::unique_ptr<T> entity;
            if (type == "Player") {
                auto player = new Player("", 0, 0, 0, 0);
                player->load(file);
                entity.reset(player);
            } else if (type == "Enemy") {
                auto enemy = new Enemy("", 0, 0, 0, "");
                enemy->load(file);
                entity.reset(enemy);
            } else {
                throw std::runtime_error("Unknown entity type in file");
            }

            entities.push_back(std::move(entity));
        }
    }
};

int main() {
    try {
        // Создаем менеджер и добавляем персонажей
        GameManager<Entity> manager;
        manager.addEntity(new Player("Hero", 100, 20, 10, 50));
        manager.addEntity(new Enemy("Goblin", 50, 15, 5, "Goblin"));
        manager.addEntity(new Enemy("Dragon", 200, 30, 20, "Boss"));

        std::cout << "Original entities:\n";
        manager.displayAll();

        // Сохраняем в файл
        manager.saveToFile("game_save.txt");
        std::cout << "\nEntities saved to file.\n";

        // Загружаем из файла в новый менеджер
        GameManager<Entity> loadedManager;
        loadedManager.loadFromFile("game_save.txt");
        std::cout << "\nLoaded entities:\n";
        loadedManager.displayAll();

    } catch (const std::exception& e) {
        std::cerr << "Error: " << e.what() << std::endl;
        return 1;
    }

    return 0;
}
