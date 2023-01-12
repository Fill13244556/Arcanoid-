#pragma once
#include "SFML/Graphics.hpp"
#include "bat.h"
#include "ball.h"
#include "settings.h"


void checkEvents(sf::RenderWindow& window, Ball& ball) {
	sf::Event event;
	while(window.pollEvent(event)) {
		if (event.type == sf::Event::Closed )
			window.close();
		if (ball.shape.getPosition().y >= (WINDOW_HEIGHT - 2 * BALL_RADIUS))
		{
			getchar();
		}
	}
}

void updateGame(Bat& bat, Ball& ball) {
	batControl(bat);
	batReboundEdges(bat);
	moveBall(ball);
	ballControl(ball,bat);
}

void checkCollisions() {}

void drawGame(sf::RenderWindow& window, Bat& bat, Ball& ball) {
	window.clear();
	batDraw(window, bat);
	ballDraw(window, ball);
	window.display();
}
void initText(sf::Text& ScoreText, int Score, sf::Font& font, const int charSize, const sf::Vector2f textstartpos) {
	ScoreText.setString(std::to_string(Score));
	ScoreText.setFont(font);
	ScoreText.setCharacterSize(charSize);
	ScoreText.setPosition(textstartpos);
}

